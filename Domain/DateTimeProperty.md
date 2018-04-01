# DateTime Property
M# DateTime is a high level representation of a date. By adding a DateTime property, M# will generates a standard C# DateTime property with its XML documentation:

```C#
/// <summary>Gets or sets the value of DateOfBirth on this Employee instance.</summary>
public DateTime DateOfBirth { get; set; }
```

The creation of this property will also create the **datetime** SQL type. M# gives you flexibility by defining some specific DateTime methods allowing you to change the behaviour in your C# logic or the generated SQL code.

## Methods

| Methods                     | Sample                               | Description                                                                                       |
|:----------------------------|:-------------------------------------|:--------------------------------------------------------------------------------------------------|
| .HasDate(bool value = true) | DateTime("Date of birth").HasDate(); | Has date will have no effect on the database column definition or the generated C# class. M# will store this as a datetime in the database. Instead of creating two integer properties for Hour and Minute, use the DateTime property and set this method to false. By doing this you will get Time validation without writing a line of code. For example the time 06:30 will be stored as "1900-01-01 06:30:00.000", corresponding to the minimum date value for SQL Server. |
| .HasTime(bool value = true) | DateTime("Date of birth").HasTime(); | Has time will have no effect on the database column definition or the generated C# class. M# will store this as a datetime in the database. This will create a Date record with the date set to 0. For example the date 01/01/2000 will be stored as "2000-01-01 00:00:00.000". |
| .LowerBound(string value)   | DateTime("Date updated").LowerBound("DateCreated");| Lower bound will have no effect on the database column definition, but will create a new validation rule based on the value. |
| .UpperBound(string value)   | DateTime("Date updated").UpperBound("DateCreated");| Upper bound will have no effect on the database column definition, but will create a new validation rule based on the value.It works exactly like Lower bound except that the value must be before the method value. |
| .UseUtcDatetimeFormat(bool? value = true) | DateTime("Date of birth").UseUtcDatetimeFormat(); | Use utc datetime format will have no effect on the database column definition, but the model population will change the date. |                                                                                  |

### Sample Codes

#### .LowerBound()
Lower bound will have no effect on the database column definition, but will create a new validation rule based on the value. For example if you create the properties "DateAdded" and "DateUpdated" you can set the lower bound of DateUpdated to DateAdded:

```C#
DateTime("Date created").Mandatory();

DateTime("Date updated").Mandatory().LowerBound("DateCreated");
```

```C#
if (DateUpdated < DateCreated)                
            result.Add("The provided Date updated is too early.");
```

### LocalTime
Testing the behaviour of an application at different dates in not easy, but we often have to do this. With the M# LocalTime class it becomes easy to manipulate and control dates in a test environment. LocalTime is not a type like DateTime is, but more like a new class surrounding DateTime, returning DateTime result and providing you some new features.

#### How to use it?
Forget using the DateTime class for getting the Date/Time, replace it by LocalTime everywhere in your code to benefit from the power of LocalTime. You can for example change the datetime of your application by using `LocalTime.Set()`. This method implements IDisposable so it is very easy to change the datetime only on a piece of code as shown on the following code:

```C#
// LocalTime.Now = 01/04/2018
using (LocalTime.Set(LocalTime.Now.AddYears(1)))
{
    // LocalTime.Now = 01/04/2019
}
// LocalTime.Now = 01/04/2018
```

You may also be interested by `LocalTime.RedifineNow()` to set the current time of the application.

Another useful feature is `LocalTime.Stop()`. By using this you can stop the datetime:

```C#
using (LocalTime.Stop())
{
    // Action 1
    // Action 2
    // Action 3
    // ...
}
```

#### Advantages
There are lots of advantages, but most of them are on test environment:
- Returns a `DateTime` type, compatible with all DateTime extension methods.
- Test server: Check the behaviour of the application over time, for example the generation of monthly invoices.
- Unit test: Run all your tests at the same time, or change the date/time to test a different scenario.
