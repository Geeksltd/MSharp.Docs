# Default image URL

## Problem

In some cases, even if no image exists in an entity when you are displaying it, you might want to show some default image.
This is the case for example when a user has no profile picture.
M# allows you to choose different default images for different entities easily.

## Implementation

The `DefaultValueUrl()` method of the `SecureImage` property allows you to specify the default URL of the image which is used for display purposes in ASP.NET pages only.
It has no effect on the database column.

#### Example

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

As you can see we set the `DefaultValueUrl()` of the image using a URL to an image asset on the web.
Whenever the image wasn't present in an entity of type `Product`, this URL is used as the image for display purposes.