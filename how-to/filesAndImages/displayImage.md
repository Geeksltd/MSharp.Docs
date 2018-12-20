# Displaying an images

## Problemm

When you display an entity which contains an image in the UI, you usually want to display the image that the entity refers to instead of the address of the image.
Naturally M# allows you to do that.

## Implementation

The `ImageColumn()` method can be used to display an image in the list module.
The `ImageUrl()` method should be used on the image column to set the URL of the image.
Usually in a list you use the `@item` property to access the current item of the list.

#### Example

Let's say we want to display a list of products and each product has a name and an image.

The product looks like this

```csharp
using MSharp;


namespace Domain
{
    public class Product : EntityType
    {
        public Product()
        {
            String("Product Name").Mandatory();
            SecureImage("Photo").Mandatory().DefaultValueUrl("http://www.example.com/image.jpg");
        }
    }
}
```

The code for the list module would look like this


```csharp
using MSharp;

namespace Modules
{
    public class ProductsList : ListModule<Domain.Product>
    {
        public ProductsList()
        {
            ImageColumn("Photo").ImageUrl("@item.Photo");
            Column(x => x.ProductName);
        }
    }
}
```

`@item.Photo` means the `Photo` property of the current image.
As you can see `ImageColumn` in combination with the `ImageUrl()` method allows us to display images in our UI modules.