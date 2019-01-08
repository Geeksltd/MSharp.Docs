# Secure Access

## Problem

Sometimes, you need to show a file to the end users even if they are unauthorized, by default all files are secure and after authorization users have access to the file, so M# will handle this behaviour by `.SecureAccess()` method.

#### Example

Let's say we have a product which has a name, an image and thumbnail properties. we what to show the thumbnail of the project to anyone and we don't plan to have any security for this property.

```csharp
using MSharp;

namespace Domain
{
    public class Product : EntityType
    {
        public Product()
        {
            String("Name").Mandatory();
            SecureImage("Photo").Mandatory().ValidExtensions("png,jpg").SecureAccess();
            SecureImage("Thumbnail").OptimizationQuality(70).Width(100).Height(50).SecureAccess(false);
        }
    }
}

```

As you can see, we have used `.SecureAccess()` method which will manage file access permission. by setting `false` there would be no protection on the file and it's available for anyone.