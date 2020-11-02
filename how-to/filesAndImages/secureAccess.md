# Secure Access

## Problem

Sometimes, you need to show a file to the end users even if they are unauthorized, by default all files are secure and after authorization users have access to the file, so M# will handle this behaviour by `.SecureAccess()` method.

#### Example

Let's say we have a product which has a name, an image and thumbnail properties. We what to show the thumbnail of the project to anyone and we don't plan to have any security for this property.

```csharp
using MSharp;

namespace Domain
{
    public class Product : EntityType
    {
        public Product()
        {
            String("Name").Mandatory();
            SecureImage("Photo").SecureAccess();
            SecureImage("Thumbnail").SecureAccess();
        }
    }
}

```

As you can see, we have used `.SecureAccess()` method which will manage file access permission. By setting `false` there would be no protection on the file and it's available for anyone.