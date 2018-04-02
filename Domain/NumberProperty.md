# Number Property
M# Number is a high level representation of a number. By adding a Numeric property, M# will generate a standard C# int/double property with its XML documentation. M# gives you flexibility by using some specific Numeric methods allowing you to change the behaviour in your C# logic or the generated SQL code.

### M# list of different numeric methods:
- `Int()`
- `Decimal()`
- `Double()`
- `Money()`
- `Percent()`

## Methods

| Methods                                | Sample                                               | Description                                                     |
|:---------------------------------------|:-----------------------------------------------------|:----------------------------------------------------------------|
| .IsCurrency(bool value = true)         | Double("Amount").IsCurrency().Scale(2);              | The currency method automatically displays the currency symbol next to the amount in all M# generated UIs. It has no effect on the database column definition or the generated C# class. |
| .IsPercentage(bool value = true)       | Double("Rate").IsPercentage().Scale(2).Max(100);     | The percentage method automatically displays the percentage symbol next to the number in all M# generated UIs. It has no effect on the database column definition or the generated C# class. |
| .Min(int\decimal\double\string value); | Int("Age").Min(25);                                  | Min will have no effect on the database column definition. That will only add a new validation rule to your entity to make sure that the number entered is not less than your value. For example if the user must be 25 or older, you can set this method to 25. |
| .Scale(int value)                      | Double("Average").Scale(2);                          | Scale represents the precision of the number. The generated C# Type will be a Double and the SQL column type a numeric(27,2) if your scale is 2. |
| .Max(int\decimal\double\string value)  | Int("Age").Max(60);                                  | Upper bound will have no effect on the database column definition. Instead a new validation rule will be added to your entity to make sure that the number entered is not more than your value. For example if the user must be a maximum of 60 years old, you can set this method to 60. |

