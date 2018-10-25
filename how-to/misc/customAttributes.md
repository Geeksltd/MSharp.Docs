# Custom [Attributes]

## Problem

There are attributes in .NET or your own developed tools which you might want to put them on your entity properties.
Examples are: JSON/XML serialization ones, custom tools attributes and ...

In M# you can easily declare attributes for your entity properties.

## Implementation

Custom attributes can be declared by using the `Attributes()` method on the property.
As argument, it takes the exact attribute definition like `[Serializable]` or `[XMLIgnore]`.

#### Example

We have an employee entity which we want to serialize to XML but some of its properties should not be serialized.
The `AdditionalNotes` property of our employee class is not important for serialization to the XML format since we use the format for archiving and we only save very important information in the archive.
We define the `Employee` entity like this

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
            String("Additional notes").Attributes("[XmlIgnore]");
        }
    }
}
```

#### Generated Code

The generated code of the employee is presented below.

```csharp
public partial class Employee : GuidEntity
{
        /* -------------------------- Properties -------------------------*/
        
        /// <summary>Gets or sets the value of AdditionalNotes on this Employee instance.</summary>
        [XmlIgnore]
        public string AdditionalNotes { get; set; }
        
        /// <summary>Gets or sets the value of FirstName on this Employee instance.</summary>
        [System.ComponentModel.DisplayName("first Name")]
        public string FirstName { get; set; }
        
        /// <summary>Gets or sets the value of LastName on this Employee instance.</summary>
        [System.ComponentModel.DisplayName("Last Name")]
        public string LastName { get; set; }
}
```

As it can be seen above, the `AdditionalNotes` property is decorated with the `[XmlIgnore]` attribute.