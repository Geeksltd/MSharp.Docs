# Text Pattern and Regex

## Problem

Many of the text inputs which a program uses, should have specific patterns.
They for example should be a phone number, email address, postal code or ...
You usually should be able to validate them both at the client and on the server.
M# has a very easy to use feature for allowing this.

## Implementation

You should call `Accepts()` method on any `String()` property which you want to define a specific pattern for it.
After you call `Accepts()` then you can choose a pattern from the available `TextPattern` values.
They include:

- Email address
- social security ID
- company ID (US/UK/Scotland
- ISBN
- Postal Code
- ...
Then M# generates correct validation code for you using Regex (regular expressions) so the content of the property has the valid pattern.


#### Example

Let's say we want to define an employee entity which has a name and an email address.
We define the entity like this

```csharp
using MSharp;

namespace Model
{
    public class Employee : EntityType
    {
        public Employee()
        {
            String("first Name").Mandatory();
            String("Last Name").Mandatory();
            String("Email").Mandatory().Accepts(TextPattern.EmailAddress);
        }
    }
}

```

As you can see we call `Accepts()` method on the `Email` property and tell M# that it accepts an email address as a valid pattern.

#### Generated Code

The code generated for the `ValidateProperties()` method of the `Employee` entity looks like this:

```csharp
protected override Task ValidateProperties()
        {
            var result = new List<string>();
            
            if (Email.IsEmpty())
                result.Add("Email cannot be empty.");
            
            if (Email?.Length > 200)
                result.Add("The provided Email is too long. A maximum of 200 characters is acceptable.");
            
            // Ensure Email matches Email address pattern:
            
            if (Email.HasValue() && !System.Text.RegularExpressions.Regex.IsMatch(Email, "\\s*\\w+([-+.'\\w])*@\\w+([-.]\\w+)*\\.\\w+([-.]\\w+)*\\s*"))
                result.Add("The provided Email is not a valid Email address.");
            
            if (FirstName.IsEmpty())
                result.Add("first Name cannot be empty.");
            
            if (FirstName?.Length > 200)
                result.Add("The provided first Name is too long. A maximum of 200 characters is acceptable.");
            
            if (LastName.IsEmpty())
                result.Add("Last Name cannot be empty.");
            
            if (LastName?.Length > 200)
                result.Add("The provided Last Name is too long. A maximum of 200 characters is acceptable.");
            
            if (result.Any())
                throw new ValidationException(result.ToLinesString());
            
            return Task.CompletedTask;
        }
```

The generated code compares the string value with the regular expression for email address pattern and if the pattern is not valid then throws an exception.