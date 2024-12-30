# Domain Languages

Computer languages influence how you think about a problem, and how you
think about communicating. Every language comes with a list of features:
buzzwords such as static versus dynamic typing, early versus late binding,
functional versus OO, inheritance models, mixins, macros—all of which may
suggest or obscure certain solutions. Designing a solution with C++ in mind
will produce different results than a solution based on Haskell-style thinking,
and vice versa. Conversely, and we think more importantly, the language of
the problem domain may also suggest a programming solution.

We always try to write code using the vocabulary of the application domain.
In some cases, Pragmatic Programmers
can go to the next level and actually program using the vocabulary, syntax,
and semantics—the language—of the domain.

## Some Real-World Domain Languages

Let’s look at a few examples where folks have done just that.

### RSpec

RSpec is a testing library for Ruby. It inspired versions for most other modern
languages. A test in RSpec is intended to reflect the behavior you expect from
your code.

```ruby
describe BowlingScore do
    it "totals 12 if you score 3 four times" do
        score = BowlingScore.new
        4.times { score.add_pins(3) }
        expect(score.total).to eq(12)
    end
end
```

### Cucumber

Cucumber is programming-language neutral way of specifying tests. You
run the tests using a version of Cucumber appropriate to the language you’re
using. In order to support the natural-language like syntax, you also have to
write specific matchers that recognize phrases and extract parameters for the
tests.

```gherkin
Feature: Scoring

Background:
Given an empty scorecard

Scenario: bowling a lot of 3s
Given I throw a 3
And I throw a 3
And I throw a 3
And I throw a 3
Then the score should be 12
```

Cucumber tests were intended to be read by the customers of the software
(although that happens fairly rarely in practice; the following aside considers
why that might be).

:::tip
Why Don’t Many Business Users Read Cucumber Features?

One of the reasons that the classic gather requirements, design, code, ship approach
doesn’t work is that it is anchored by the concept that we know what the requirements
are. But we rarely do. Your business users will have a vague idea of what they want
to achieve, but they neither know nor care about the details. That’s part of our value:
we intuit intent and convert it to code.
So when you force a business person to sign off on a requirements document, or get
them to agree to a set of Cucumber features, you’re doing the equivalent of getting
them to check the spelling in an essay written in Sumerian. They’ll make some random
changes to save face and sign it off to get you out of their office.
Give them code that runs, however, and they can play with it. That’s where their real
needs will surface.
:::

### Phoenix Routes

Many web frameworks have a routing facility, mapping incoming HTTP
requests onto handler functions in the code. Here’s an example from Phoenix.

```ruby
scope "/", HelloPhoenix do
    pipe_through :browser # Use the default browser stack

    get "/", PageController, :index
    resources "/users", UserController
end
```

This says that requests starting “/” will be run through a series of filters
appropriate for browsers. A request to “/” itself will be handled by the index
function in the PageController module. The UsersController implements the functions
needed to manage a resource accessible via the url /users.

### Ansible

Ansible is a tool that configures software, typically on a bunch of remote
servers. It does this by reading a specification that you provide, then doing
whatever is needed on the servers to make them mirror that spec. The speci-
fication can be written in YAML, a language that builds data structures from
text descriptions:

```yaml
---
- name: install nginx
apt: name=nginx state=latest
- name: ensure nginx is running (and enable it at boot)
service: name=nginx state=started enabled=yes
- name: write the nginx config file
template: src=templates/nginx.conf.j2 dest=/etc/nginx/nginx.conf
notify:
- restart nginx
```

This example ensures that the latest version of nginx is installed on my
servers, that it is started by default, and that it uses a configuration file that
you’ve provided.

## Characteristics of Domain Languages

Let’s look at these examples more closely.
RSpec and the Phoenix router are written in their host languages (Ruby and
Elixir). They employ some fairly devious code, including metaprogramming
and macros, but ultimately they are compiled and run as regular code.
Cucumber tests and Ansible configurations are written in their own languages.
A Cucumber test is converted into code to be run or into a datastructure,
whereas Ansible specs are always converted into a data structure that is run
by Ansible itself.
As a result, RSpec and the router code are embedded into the code you run:
they are true extensions to your code’s vocabulary. Cucumber and Ansible
are read by code and converted into some form the code can use.
We call RSpec and the router examples of _internal domain languages_, while
Cucumber and Ansible use _external languages_.

## Trade-Offs Between Internal and External Languages

In general, an internal domain language can take advantage of the features
of its host language: the domain language you create is more powerful, and
that power comes for free. For example, you could use some Ruby code to
create a bunch of RSpec tests automatically. In this case we can test scores
where there are no spares or strikes:

```ruby
describe BowlingScore do
    (0..4).each do |pins|
        (1..20).each do |throws|
            target = pins * throws

            it "totals #{target} if you score #{pins} #{throws} times" do
                score = BowlingScore.new
                throws.times { score.add_pins(pins) }
                expect(score.total).to eq(target)
            end
        end
    end
end
```

That’s 100 tests you just wrote. Take the rest of the day off.
The downside of internal domain languages is that you’re bound by the syntax
and semantics of that language. Although some languages are remarkably
flexible in this regards, you’re still forced to compromise between the language
you want and the language you can implement.
Ultimately, whatever you come up with must still be valid syntax in your
target language. Languages with macros (such as Elixir, Clojure, and Crystal)
gives you a little more flexibility, but ultimately syntax is syntax.
External languages have no such restrictions. As long as you can write a
parser for the language, you’re good to go. Sometimes you can use someone
else’s parser (as Ansible did by using YAML), but then you’re back to making
a compromise.
Writing a parser probably means adding new libraries and possibly tools to
your application. And writing a good parser is not a trivial job. But, if you’re
feeling stout of heart, you could look at parser generators such as bison or
ANTLR, and parsing frameworks such as the many PEG parsers out there.
Our suggestion is fairly simple: don’t spend more effort than you save. Writing
a domain language adds some cost to your project, and you’ll need to be
convinced that there are offsetting savings (potentially in the long term).
In general, use off-the-shelf external languages (such as YAML, JSON, or
CSV) if you can. If not, look at internal languages. We’d recommend using
external languages only in cases where your language will be written by the
users of your application.

## An Internal Domain Language on the Cheap

Finally, there’s a cheat for creating internal domain languages if you don’t
mind the host language syntax leaking through. Don’t do a bunch of
meta-programming. Instead, just write functions to do the work. In fact, this
is pretty much what RSpec does:

```ruby
describe BowlingScore do
    it "totals 12 if you score 3 four times" do
        score = BowlingScore.new
        4.times { score.add_pins(3) }
        expect(score.total).to eq(12)
    end
end
```

In this code, describe, it, expect, to, and eq are just Ruby methods. There’s a little
plumbing behind the scenes in terms of how objects are passed around, but
it’s all just code. We’ll explore that a little in the exercises.

## References

- The Pragmatic Programmer 2nd Edition - Andrew Hunt, David Thomas - Addison-Wesley
