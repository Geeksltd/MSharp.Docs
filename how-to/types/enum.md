# How to: Creating an Enum (reference) type

## Problem:

In almost all applications there are concepts which only can have a set of pre-defined values.
Types of phone number, list of locations, days of the week and many other examples come to mind.
There are multiple ways to deal with these but the way that most programming languages deal with them are enums, strings, numeric values or constants of them.

When dealing with them you should make sure of multiple things

- You can easily refer to them in your code without sacrificing readability or making mistakes
- You can modify the set of pre-defined values if needed without breaking everything
- You can serialize them and store them in a database easily and modifications don't create issues for your databases/serialization code

In C# most people use enums for these sets, but while convenient, they have their own challenges which we try to eliminate.

## The M# way

The way that we deal with them in M# is using specific entities for each set of values. Compared to enums it has advantages below

- enums are integers and modifying them would need a lot of care in ordering to not break compatibility
- you cannot add any other properties to an enum and adding methods require trickeries like extension methods
- Renaming enum elements potentially can break serialization code or older databases if you don't migrate them

## How to implement

To represent such a concept in M# we usually define an entity with a single string field called name.
Then each member of the set of values can be an instance of this entity type with a unique name.
Because these values are predefined, we need to create them in the database before the application starts.
The place to add these values to our database is the `ReferenceData.cs` file in the project Domain>[DEV-SCRIPTS].
You need to simply add an entity per distinct value you need in the set.

#### Example

Let's say we want to represent different types of contacts in an application.
Each contacontact can be either a friend, family member, business relation or another type of contact.
We need to create an entity with a `Name1 field like this.n

```csharp

using MSharp;

namespace Model
{
    public class ContactType : EntityType
    {
        public ContactType()
        {
            String("Name").Mandatory();
        }
    }
}
```

Then we need to open `[DEV-SCRIPTS]/ReferenceData.cs` in the **Domains** project and add all of our values in a separate method.
We will end up with something like this

```csharp

using ...;

namespace Domain
{
    class ReferenceData 
    {
        ...
        
        public async Task Create()
        {
            ...
            await CreateContactTypes();
        }
        
        ...
        
        async Task CreateContactTypes()
        {
            await Create(new ContactType { Name = "Friend" });
            await Create(new ContactType { Name = "Family" });
            await Create(new ContactType { Name = "Business" });
            await Create(new ContactType { Name = "Other" });
        }
    }
}

```

Be careful to don't forget to call the method you create in the `Create()` method where other helper methods are called.

#### Generated code

The generated code for the entity is a simple class

```ccsharp

namespace Domain
{
    using System;
    using System.Collections;
    using System.Collections.Generic;
    using System.Linq;
    using System.Threading.Tasks;
    using System.Xml.Serialization;
    using Olive;
    using Olive.Entities;
    using Olive.Entities.Data;
    
    /// <summary>Represents an instance of Contact type entity type.</summary>
    [EscapeGCop("Auto generated code.")]
    public partial class ContactType : GuidEntity
    {
        /* -------------------------- Properties -------------------------*/
        
        /// <summary>Gets or sets the value of Name on this Contact type instance.</summary>
        public string Name { get; set; }
        
        /* -------------------------- Methods ----------------------------*/
        
        /// <summary>Returns a textual representation of this Contact type.</summary>
        public override string ToString() => Name;
        
        /// <summary>Returns a clone of this Contact type.</summary>
        /// <returns>
        /// A new Contact type object with the same ID of this instance and identical property values.<para/>
        ///  The difference is that this instance will be unlocked, and thus can be used for updating in database.<para/>
        /// </returns>
        public new ContactType Clone() => (ContactType)base.Clone();
        
        /// <summary>
        /// Validates the data for the properties of this Contact type and throws a ValidationException if an error is detected.<para/>
        /// </summary>
        protected override Task ValidateProperties()
        {
            var result = new List<string>();
            
            if (Name.IsEmpty())
                result.Add("Name cannot be empty.");
            
            if (Name?.Length > 200)
                result.Add("The provided Name is too long. A maximum of 200 characters is acceptable.");
            
            if (result.Any())
                throw new ValidationException(result.ToLinesString());
            
            return Task.CompletedTask;
        }
    }
}

```

## Remarks

- We usually show these pre-defined sets as DropDowns in forms or modules
