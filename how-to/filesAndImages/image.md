# Handling Images

## Problem

Some entities need to contain images.
An image is a file but M# can support additional features for an image.
In this page we'll talk about how M# helps you to work with images.

## implementation

When defining your entity, `SecureImage` allows you to have an image file as a property which can be entered in forms and displayed and ...

#### Example

Let's say we have a product which has a name and an image as its properties.
We define it like this

```csharp
using MSharp;


namespace Domain
{
    public class Product : EntityType
    {
        public Product()
        {
            String("Product Name").Mandatory();
            SecureImage("Photo").Mandatory().ValidExtensions("png, bmp");
        }
    }
}

```

As you can see, we use the `SecureImage` to define the product photo property.

#### Generated Code

The generated code for the entity looks like this

```csharp
public partial class Product : GuidEntity
{
        /// <summary>Stores the binary information for Photo property.</summary>
        private Blob photo;
        
        /// <summary>
        /// Gets or sets the value of Photo on this Product instance.<para/>
        /// When a download request comes, the system will call my method IsPhotoVisibleTo(IUser) which must return True for only permitted users.<para/>
        /// </summary>
        [Newtonsoft.Json.JsonIgnore]
        [SecureFile]
        public Blob Photo
        {
            get
            {
                if (photo is null) photo = Blob.Empty().Attach(this, "Photo");
                return photo;
            }
            
            set
            {
                if (!(photo is null))
                {
                    // Detach the previous file, so it doesn't get updated or deleted with this Product instance.
                    photo.Detach();
                }
                
                if (value is null)
                {
                    value = Blob.Empty();
                }
                else
                {
                    value.OptimizeImage(10000, 10000, 75);
                }
                
                photo = value.Attach(this, "Photo");
            }
        }
        
        /// <summary>Gets or sets the value of ProductName on this Product instance.</summary>
        [System.ComponentModel.DisplayName("Product Name")]
        public string ProductName { get; set; }
        
        /* -------------------------- Methods ----------------------------*/
        
        /// <summary>Returns a textual representation of this Product.</summary>
        public override string ToString() => ProductName;
        
        /// <summary>Returns a clone of this Product.</summary>
        /// <returns>
        /// A new Product object with the same ID of this instance and identical property values.<para/>
        ///  The difference is that this instance will be unlocked, and thus can be used for updating in database.<para/>
        /// </returns>
        public new Product Clone()
        {
            var result = (Product) base.Clone();
            
            result.Photo = Photo.Clone();
            return result;
        }
        
        /// <summary>
        /// Validates the data for the properties of this Product and throws a ValidationException if an error is detected.<para/>
        /// </summary>
        protected override Task ValidateProperties()
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
            
            if (result.Any())
                throw new ValidationException(result.ToLinesString());
            
            return Task.CompletedTask;
        }
}
```

There are multiple things which worth discussing:

- `Blob` data-type in M# is used to represent binary data like file content
- There is a `Blob` property and a field with the same type. The field stores the actual data and the property contains the logic to check if the content is changing to null or changing from null to a value, correct file attachment/detachments happen.
- The `Blob` property named `Photo` has a `[SecureFile]` attribute and a `JsonIgnore]` attribute which tells `JSON.Net` to skip it when serializing the entity.
- When cloning the entity, the `Photo` property is cloned separately and then the clone is referenced by the cloned object. This is because the shallow copying of the object which is used for cloning will not copy clone the blob automatically.
- There are methods in the setter of the `Photo` property for optimizing the image which will be described in the optimizations page.