# The role of ToStringExpression()

M# uses `ToString()` in a similar way to the standard `ToString()` function of a C# object, allowing a specific format to be defined, as needed for your application, but adds some features on top of this. Generated Web pages can use this function in some cases, for example this will be the text displayed in dropdown lists or used to search for a text.

### Creation

To implement ToString(), open your Entity in visual studio and select `ToStringExpression()` method. At this point, if the value is simple, you can specify the value directly, or for more complex requirements, specify a function.

```csharp
ToStringExpression("$\"Employee: {FullName}\"");
```

### Generated Code

`ToStringExpression()` will have no effect on the database column definition. A standard `ToString()` function will be written in your C# file.

```csharp
/// <summary>Returns a textual representation of this Employee.</summary>
public override string ToString() => $"Employee: { FullName}";
```