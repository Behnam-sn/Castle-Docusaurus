---
sidebar_position: 1
---

# Value Object

## What is a Value Object?

## What Problem Value Object is Trying to Solve?

Relying exclusively on the language’s standard library’s primitive data types,  
Such as strings, integers, or dictionaries,  
To represent concepts of the business domain,  
Is known as the **primitive obsession code smell**.

For example,  
Consider the following class:

```cs
class Person
{
    private int _id;
    private string _firstName;
    private string _lastName;
    private string _landlinePhone;
    private string _mobilePhone;
    private string _email;
    private int _heightMetric;
    private string _countryCode;

    public Person(...) {...}
}

static void Main(string[] args)
{
    var dave = new Person(
        id: 30217,
        firstName: "Dave",
        lastName: "Ancelovici",
        landlinePhone: "023745001",
        mobilePhone: "0873712503",
        email: "dave@learning-ddd.com",
        heightMetric: 180,
        countryCode: "BG");
}
```

In the preceding implementation of the `Person` class,  
Most of the values are of type `string` and they are assigned based on convention.

For example,  
The input to the `landlinePhone` should be a valid landline phone number,  
And the `countryCode` should be a valid, two-letter, uppercased country code.

Of course, the system cannot trust the user to always supply correct values,  
And as a result, the class has to validate all input fields.

This approach presents multiple design risks:

- First, the validation logic tends to be duplicated.
- Second, it’s hard to enforce calling the validation logic before the values are used.
- It will become even more challenging in the future,  
  When the codebase will be evolved by other engineers.

## What is Value Object Solution?

Compare the following alternative design of the same object,  
This time leveraging value objects:

```cs
class Person {
    private PersonId _id;
    private Name _name;
    private PhoneNumber _landline;
    private PhoneNumber _mobile;
    private EmailAddress _email;
    private Height _height;
    private CountryCode _country;

    public Person(...) { ... }
}

static void Main(string[] args)
{
    var dave = new Person(
        id: new PersonId(30217),
        name: new Name("Dave", "Ancelovici"),
        landline: PhoneNumber.Parse("023745001"),
        mobile: PhoneNumber.Parse("0873712503"),
        email: Email.Parse("dave@learning-ddd.com"),
        height: Height.FromMetric(180),
        country: CountryCode.Parse("BG"));
}
```

Let's review the benefits of using value objects:

- ### Clarity

  The value object makes the intent clear,  
  Even with shorter variable names.

  For example, the `country` variable.  
  There is no need to elaborately call it `countryCode`,  
  To communicate the intent of it holding a country code and not,  
  For example, a full country name.

- ### Validation

  There is no need to validate the values before the assignment,  
  As the validation logic resides in the value objects themselves.

- ### Centralized Business Logic

  Value objects shine brightest when they centralize the business logic that manipulates the values.  
  The cohesive logic is implemented in one place and is easy to test.

- ### Intuitive

  As you can see in the preceding example,  
  Value objects eliminate the need for conventions.

  For example, the need to keep in mind that this string is an email and the other string is a phone number.  
  And instead makes using the object model less error prone and more intuitive.

- ### Ubiquitous Language

  Most importantly, value objects express the business domain’s concepts:  
  They make the code speak the ubiquitous language.

## More Examples of Value Objects

Let’s see how representing the concepts of height, phone numbers, and colors as value objects,  
Makes the resultant type system rich and intuitive to use.

### Height

Compared to an integer-based value,  
The `Height` value object,  
Makes the intent clear,  
And decouples the measurement from a specific measurement unit.

For example,  
The `Height` value object can be initialized using both metric and imperial units;

Making it easy to convert from one unit to another,  
Generating string representation,  
And comparing values of different units.

```cs
var heightMetric = Height.Metric(180);
var heightImperial = Height.Imperial(5, 3);

var string1 = heightMetric.ToString();              // "180cm"
var string2 = heightImperial.ToString();            // "5 feet 3 inches"
var string3 = heightMetric.ToImperial().ToString(); // "5 feet 11 inches"

var firstIsHigher = heightMetric > heightImperial;  // true
```

### Phone Number

The `PhoneNumber` value object can encapsulate the logic of parsing a string value, validating it, and extracting different attributes of the phone number.

For example, the country it belongs to and the phone number’s type (landline or mobile):

```cs
var phone = PhoneNumber.Parse("+359877123503");
var country = phone.Country;                        // "BG"
var phoneType = phone.PhoneType;                    // "MOBILE"
var isValid = PhoneNumber.IsValid("+972120266680"); // false
```

### Color

The following example demonstrates the power of a value object when it encapsulates all of the business logic that manipulates the data and produces new instances of the value object:

```cs
var red = Color.FromRGB(255, 0, 0);
var green = Color.Green;
var yellow = red.MixWith(green);
var yellowString = yellow.ToString(); // "#FFFF00"
```

### String

Although using a core library’s Strings to represent domain-specific values contradicts the notion of value objects, in .NET, Java, and other languages the string type is implemented exactly as a value object.

Strings are immutable, as all operations result in a new instance.  
Moreover, the string type encapsulates a rich behavior that creates new instances by manipulating the values of one or more strings:  
trim, concatenate multiple strings, replace characters, substring, and other methods.

## How to Implement a Value Object?

### Identification

A value object is an object that can be identified by the composition of its values.

For example, consider a color object:

```cs
public class Color
{
    public readonly byte Red;
    public readonly byte Green;
    public readonly byte Blue;
}
```

The composition of the values of the three fields red, green, and blue defines a color.  
Changing the value of one of the fields will result in a new color.  
No two colors can have the same values.  
Also, two instances of the same color must have the same values.  
Therefore, no explicit identification field is needed to identify colors.

### Immutability

Since a change to any of the fields of a value object results in a different value,  
Value objects are implemented as immutable objects.

A change to one of the value object’s fields conceptually creates a different value (a different instance of a value object).

Therefore, when an executed action results in a new value,  
as in the following case,  
which uses the `MixWith` method,  
it doesn’t modify the original instance but instantiates and returns a new one:

```cs
public class Color
{
    public Color(byte r, byte g, byte b)
    {
        this.Red = r;
        this.Green = g;
        this.Blue = b;
    }

    public Color MixWith(Color other)
    {
        return new Color(
            r: (byte) Math.Min(this.Red + other.Red, 255),
            g: (byte) Math.Min(this.Green + other.Green, 255),
            b: (byte) Math.Min(this.Blue + other.Blue, 255)
        );
    }
}
```

Since value objects are immutable,  
The value objects behavior is free of side effects and is thread safe.

### Equality Checks

Since the equality of value objects is based on their values rather than on an id field or reference,  
it’s important to override and properly implement the equality checks.

For example:

```cs
public class Color
{
    public override bool Equals(object obj)
    {
        var other = obj as Color;
        return other != null &&
            this.Red == other.Red &&
            this.Green == other.Green &&
            this.Blue == other.Blue;
    }

    public static bool operator == (Color lhs, Color rhs)
    {
        if (Object.ReferenceEquals(lhs, null)) {
            return Object.ReferenceEquals(rhs, null);
        }
        return lhs.Equals(rhs);
    }

    public static bool operator != (Color lhs, Color rhs)
    {
        return !(lhs == rhs);
    }

    public override int GetHashCode()
    {
        return ToString().GetHashCode();
    }
}
```

## When to Use Value Objects?

The simple answer is, whenever you can.

Not only do value objects make the code more expressive,  
And encapsulate business logic that tends to spread apart,  
But the pattern makes the code safer.

From a business domain perspective,  
A useful rule of thumb is to use value objects for the domain’s elements that describe properties of other objects.

The examples you saw earlier used value objects to describe a person, including their ID, name, phone numbers, email, and so on.  
Other examples of using value objects include various statuses, passwords, and more business domain–specific concepts that can be identified
by their values and thus do not require an explicit identification field.

An especially important opportunity to introduce a value object is when modeling money and other monetary values.  
Relying on primitive types to represent money not only limits your ability to encapsulate all money-related business logic in one place, but also often leads to dangerous bugs, such as rounding errors and other precision-related issues.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
