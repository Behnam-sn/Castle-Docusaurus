<!-- # CSRF

## Overview

A **Cross-Site Request Forgery (CSRF)** is a type of cyber attack.
CSRF attack forces an user to execute unwanted actions on a web application in which they’re currently authenticated.

With a little help of social engineering (such as sending a link via email or chat),
An attacker may trick the users of a web application into executing actions of the attacker’s choosing.

If the victim is a normal user,
A successful CSRF attack can force the user to perform state changing requests like transferring funds from their account, changing their email address and password, or some other undesired action.

If the victim is an administrative account, CSRF can compromise the entire web application,
Potentially resulting in complete takeover of a web application, API, or other service.

## What is CSRF?

CSRF is an attack that tricks the victim into submitting a malicious request.
It inherits the identity and privileges of the victim,
To perform an undesired function on the victim’s behalf.

For most sites,
Browser requests automatically include any credentials associated with the site,
Such as the user’s session cookie, IP address, Windows domain credentials, and so forth.

Therefore, if the user is currently authenticated to the site,
The site will have no way to distinguish between the forged request sent by the victim and a legitimate request sent by the victim.

CSRF attacks target functionality that causes a state change on the server,
Such as changing the victim’s email address or password, or purchasing something.

Forcing the victim to retrieve data doesn’t benefit an attacker because the attacker doesn’t receive the response, the victim does.
As such, CSRF attacks target state-changing requests.

## How does Cross-Site Request Forgery work?

There are numerous ways in which a user can be tricked into loading information from or submitting information to a web application.
In order to execute an attack, we must first understand how to generate a valid malicious request for our victim to execute.

Let us consider the following example:
Alice wishes to transfer $100 to Bob using the bank.com web application that is vulnerable to CSRF.
Maria, an attacker, wants to trick Alice into sending the money to Maria instead.

The attack will comprise the following steps:

1. Building an exploit URL or script
1. Tricking Alice into executing the action with Social Engineering

Different HTTP verbs have varying vulnerability to CSRF attacks, resulting in variable protection strategies.
This is due to the way that web browsers handle the verbs differently.

### GET scenario

If the application was designed to primarily use GET requests to transfer parameters and execute actions,
The money transfer operation might be reduced to a request like:

`GET http://bank.com/transfer.do?acct=BOB&amount=100`

Maria now decides to exploit this web application vulnerability using Alice as the victim.
Maria first constructs the following exploit URL which will transfer $100,000 from Alice’s account to Maria’s account.
Maria takes the original command URL and replaces the beneficiary name with herself, raising the transfer amount significantly at the same time:

`http://bank.com/transfer.do?acct=MARIA&amount=100000`

The social engineering aspect of the attack tricks Alice into loading this URL when Alice is logged into the bank application.
This is usually done with one of the following techniques:

sending an unsolicited email with HTML content planting an exploit URL or script on pages that are likely to be visited by the victim while they are also doing online banking
The exploit URL can be disguised as an ordinary link, encouraging the victim to click it:

`<a href="http://bank.com/transfer.do?acct=MARIA&amount=100000">View my Pictures!</a>`

Or as a 0x0 fake image:

`<img src="http://bank.com/transfer.do?acct=MARIA&amount=100000" width="0" height="0" border="0">`

If this image tag were included in the email, Alice wouldn’t see anything.
However, the browser will still submit the request to bank.com without any visual indication that the transfer has taken place.

### POST scenario

The only difference between GET and POST attacks is how the attack is being executed by the victim.
Let’s assume the bank now uses POST and the vulnerable request looks like this:

```txt
POST http://bank.com/transfer.do HTTP/1.1

acct=BOB&amount=100
```

Such a request cannot be delivered using standard A or IMG tags, but can be delivered using a FORM tags:

<form action="http://bank.com/transfer.do" method="POST">

<input type="hidden" name="acct" value="MARIA"/>
<input type="hidden" name="amount" value="100000"/>
<input type="submit" value="View my pictures"/>

</form>
This form will require the user to click on the submit button, but this can be also executed automatically using JavaScript:

<body onload="document.forms[0].submit()">

<form...
Other HTTP methods
Modern web application APIs frequently use other HTTP methods, such as PUT or DELETE. Let’s assume the vulnerable bank uses PUT that takes a JSON block as an argument:

PUT http://bank.com/transfer.do HTTP/1.1

{ "acct":"BOB", "amount":100 }
Such requests can be executed with JavaScript embedded into an exploit page:

<script>
function put() {
    var x = new XMLHttpRequest();
    x.open("PUT","http://bank.com/transfer.do",true);
    x.setRequestHeader("Content-Type", "application/json");
    x.send(JSON.stringify({"acct":"BOB", "amount":100}));
}
</script>

<body onload="put()">
Fortunately, this request will not be executed by modern web browsers thanks to same-origin policy restrictions. This restriction is enabled by default unless the target web site explicitly opens up cross-origin requests from the attacker’s (or everyone’s) origin by using CORS with the following header:

Access-Control-Allow-Origin: \*

## How can an application prevent a Cross-Site Request Forgery attack?

## Synonyms

CSRF attacks are also known by a number of other names,
Including XSRF, “Sea Surf”, Session Riding, Cross-Site Reference Forgery, and Hostile Linking.
Microsoft refers to this type of attack as a One-Click attack in their threat modeling process and many places in their online documentation.

## References

- [owasp.org](https://owasp.org/www-community/attacks/csrf)
- [cloudflare.com](https://www.cloudflare.com/learning/security/threats/cross-site-request-forgery/)
- [wikipedia.org](https://en.wikipedia.org/wiki/Cross-site_request_forgery) -->
