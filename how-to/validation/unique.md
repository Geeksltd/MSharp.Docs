# Unique

## Problem

There are properties of entities which should be unique in the system.
For example an email address should be unique if it is used for logging in.
M# allows you to easily define unique properties and even provides additional features on top of it which uniqueness enables and might be useful for you.

## Implementation

You should call `Unique()` property on your property definition to declare its uniqueness.
This will cause no database related changes but the C# generated code will make sure the entity is unique when inserting/modifying the entity.
Also M# generates a `FindBy%PropertyName%()` method which can be used to find the entity by the unique property.
If no entity with the specified property cannot be found, `null` will be returned.

#### Example

Let's define a product class which its name should be unique.
no two products with the same name should be added to our system.

```csharp
using MSharp;


namespace Model
{
    public class Product : EntityType
    {
        public Product()
        {
            Int("Cost").Mandatory();
            String("Product Name").Mandatory().Unique();
        }
    }
}

```

We call `Unique()` on the name property so only products with unique names are allowed.

#### Generated Code

The generated code is interesting to look at

```csharp

public partial class Product : GuidEntity
{
        /// <summary>Gets or sets the value of Cost on this Product instance.</summary>
        public int Cost { get; set; }
        
        /// <summary>Gets or sets the value of ProductName on this Product instance.</summary>
        [System.ComponentModel.DisplayName("Product Name")]
        public string ProductName { get; set; }
        

        /// <summary>
        /// Find and returns an instance of Product from the database by its Product Name.<para/>
        ///                               If no matching Product is found, it returns Null.<para/>
        /// </summary>
        /// <param name="productName">The Product Name of the requested Product.</param>
        /// <returns>
        /// The Product instance with the specified Product Name or null if there is no Product with that Product Name in the database.<para/>
        /// </returns>
        public static Task<Product> FindByProductName(string productName)
        {
            return Database.FirstOrDefault<Product>(p => p.ProductName == productName);
        }
        
        /// <summary>
        /// Validates the data for the properties of this Product and throws a ValidationException if an error is detected.<para/>
        /// </summary>
        protected override async Task ValidateProperties()
        {
            var result = new List<string>();
            
            if (Cost < 0)
                result.Add("The value of Cost must be 0 or more.");
            
            if (ProductName.IsEmpty())
                result.Add("Product Name cannot be empty.");
            
            if (ProductName?.Length > 200)
                result.Add("The provided Product Name is too long. A maximum of 200 characters is acceptable.");
            
            // Ensure uniqueness of ProductName.
            
            if (await Database.Any<Product>(p => p.ProductName == ProductName && p != this))
                result.Add("Product Name must be unique. There is an existing Product record with the provided Product Name.");
            
            if (result.Any())
                throw new ValidationException(result.ToLinesString());
        }
}

```

As you can see a `FindByProductName()` method is generated which allows you to search the database by using a product name. 
It either returns a product or null if no product can be found.

Also in the `ValidateProperties()` method, the code checks to see if the product name is unique or not by using a `Any` operation.