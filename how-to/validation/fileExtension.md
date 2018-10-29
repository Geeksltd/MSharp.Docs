# Allowed file extensions

## Problem

When you allow users to uplaod files to your website, you usually only can process a limited set of formats.
Also from a security point of view, it is not a good idea to allow users to upload any type of arbitrary file to the web application.
M# allows you to choose the valid extensions of the files when you insert an upload control in a page.

## Implementation

Let's define a product page which allows the user to upload an image of the product with its name to the server.
Then we will limit the accepted formats to png and bmp.

```csharp
using MSharp;


namespace Domain
{
    public class Product : EntityType
    {
        public Product()
        {
            String("Product Name").Mandatory().Unique();
            SecureImage("Photo").Mandatory().ValidExtensions("png, bmp");
        }
    }
}

```

As you can see we specified the valid extensions using a string of `,` separated extensions.

#### Generated Code

The generated code looks like this

```csharp
public partial class Product : GuidEntity
{
        /// <summary>Stores the binary information for Photo property.</summary>
        private Blob photo;
        
        
        /// <summary>Gets or sets the value of ProductName on this Product instance.</summary>
        [System.ComponentModel.DisplayName("Product Name")]
        public string ProductName { get; set; }
        
        ...        

        /// <summary>
        /// Validates the data for the properties of this Product and throws a ValidationException if an error is detected.<para/>
        /// </summary>
        protected override async Task ValidateProperties()
        {
            var result = new List<string>();
            
            if (Photo.IsEmpty())
            {
                result.Add("It is necessary to upload Photo.");
            }
            
            if (!new[] { "png", "bmp" }.Contains(Photo.FileExtension.ToLower().TrimStart('.')))
            {
                result.Add("Only files of the following types are accepted: png and bmp");
            }
            
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

The `ValidateProperties()` method checks the extensions of the file to be one of the valid ones we specified.