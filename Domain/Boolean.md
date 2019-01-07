# Boolean
M# Boolean is a high level representation of a boolean. By adding a Boolean property, M# will generate a standard C# bool property with its XML documentation. M# gives you flexibility by using some specific Boolean attributes allowing you to change the behaviour in your C# logic.

## Creation
Type and select `Bool` to create the property.

```csharp
using MSharp;

namespace Domain
{
    public class Employee : SubType<User>
    {
        public Employee()
        {
            Bool("Is activated").Mandatory();
        }
    }
}
```

## Methods

| Methods      | Sample     | Description        |
|:-------------|:-----------|:-------------------|
| .FalseText(string value)               | `Bool("Is activated") .FalseText("No");`                | False text will have no effect on the database column definition or the generated C# class. This will only replace the False value with your custom value in UI modules. For example you may set this text value as `No` to change all your forms using this property. If your control for this property is a radio button list the false text will be `No`.|
| .NullText(string value)                |`Bool("Is activated") .NullText("Registeration not yet completed");`| Null text will have no effect on the database column definition or the generated C# class. This will only replace the Null value with  your custom value in UI modules. For example you may set this text value as **Registration not yet completed** to change all your forms using this property. If your control for this property is a radio button list the null text will be **Registration not yet completed**. |
| .TrueText(string value)                |` Bool("Is activated") .TrueText("Yes");`                | True text will have no effect on the database column definition or the generated C# class. This will only replace the True value with your custom value in UI modules. For example you may set this text value as `Yes` to change all your forms using this property. If your control for this property is a radio button list the true text will be `Yes`. |


Sample Test for [nav2](../Domain/Advanced/IEntityInterface.md)

sampe content
