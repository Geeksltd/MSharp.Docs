# Custom typ (C#/DB)

## Problem

M# automatically uses specific types for each property type in C# and in the database.
Sometimes you might want to use a different type in the database or in C#.
M# allows you to customize both types and even generate conversion code without coding.

## Implementation

- To use a different C# type for your property, call the `CSharpTypeName()` method.
- To change the database column's type, call `DatabaseType()` method.
- To generate conversion code between the database type and C# type, call `NeedsDatabaseTypeConversion()` method.

### Database types and conversion

#### Example

Let's use the features to modify the data-types used for a property.
A normal employee class would look like this.

```csharp
using MSharp;

namespace Model
{
    public class Employee : EntityType
    {
        public Employee()
        {
            String("First name").Mandatory();
            String("Last name").Mandatory();
        }

    }
}

```
Let's tell the database to store it as text.

```csharp
using MSharp;

namespace Model
{
    public class Employee : EntityType
    {
        public Employee()
        {
            String("First name").Mandatory().DatabaseType("text").NeedsDatabaseTypeConversion();
            String("Last name").Mandatory().DatabaseType("text").NeedsDatabaseTypeConversion();
        }

    }
}

```

#### Generated code

Let's take a look at the generated data access layer code for both.
The generated data access layer (DAL) code can be found in the `Domain` project in the `[GEN-DAL]` folder.
The important function here is the one which reads the fields from the database columns.

This is the first `Employee` without any datatype changes/conversions.

```csharp
public class EmployeeDataProvider : SqlDataProvider<Domain.Employee>
{
        ...
        internal void FillData(IDataReader reader, Domain.Employee entity)
        {
            var values = new object[reader.FieldCount];
            reader.GetValues(values);
            
            entity.FirstName = values[Fields.FirstName] as string;
            entity.LastName = values[Fields.LastName] as string;
        }
        ...
}
```

It simply casts each read value to the expected datatype.

Now let's look at the one which we store its strings as `text` in the database and then convert back to `string` in DAL code.

```csharp
public class EmployeeDataProvider : SqlDataProvider<Domain.Employee>
{
        ...
        internal void FillData(IDataReader reader, Domain.Employee entity)
        {
            var values = new object[reader.FieldCount];
            reader.GetValues(values);
            
            entity.FirstName = Convert.ToString(values[Fields.FirstName]);
            entity.LastName = Convert.ToString(values[Fields.LastName]);
        }
        ...
}
```

This one uses `Convert` family of methods for each datatype to successfully convert between datatypes.

### C# type name

The C# type  of a property can be changed as well.
You for example might want to store a set of integer numbers as `long` datatype instead of `int`. 
It can be achieved by using the `CSharpTypeName()` method as said before.

#### Example

If we define our properties as `Int()` in the entity definition, then the generated code uses `int` as the datatype for properties.
If we know we need a bigger range and want to use `long, we should do this both for the database and the class like this:

```csharp
using MSharp;

namespace Model
{
    public class Position : EntityType
    {
        public Position()
        {
            Int("X").Mandatory().CSharpTypeName("long").DatabaseType("long");
            Int("Y").Mandatory().Scale(3).CSharpTypeName("long").DatabaseType("long"); 
            Int("Z").Mandatory().Scale(3).CSharpTypeName("long").DatabaseType("long"); 
        }
    }
}
```

#### Generated Code

The generated code looks like this:

```csharp
    public partial class Position : GuidEntity
    {
       /// <summary>Gets or sets the value of X on this Position instance.</summary>
        public long X { get; set; }
        
        /// <summary>Gets or sets the value of Y on this Position instance.</summary>
        public long Y { get; set; }
        
        /// <summary>Gets or sets the value of Z on this Position instance.</summary>
        public long Z { get; set; }
    }
```

The generated code uses `long` datatype and the DAL code doesn't need conversion either.
Let's check its `FillData()` method

```csharp
internal void FillData(IDataReader reader, Domain.Position entity)
        {
            var values = new object[reader.FieldCount];
            reader.GetValues(values);
            
            entity.X = (long)values[Fields.X];
            entity.Y = (long)values[Fields.Y];
            entity.Z = (long)values[Fields.Z];
        }
```


## Remarks

- Don't use this feature if you really don't need it, it Complicates your code.
- Conversion between all types is not possible, be careful about data loss when choosing datatypes.
