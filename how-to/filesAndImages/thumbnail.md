# Thumbnail

## Problem

Sometimes, you need to show a thumbnail image of a bigger image. this thumbnail should be same as original image but more optimized with smaller size and dimension.

## Implementation

To implement thumbnail we should use `.OptimizationQuality()`, `.Width()` and `.Height()` methods to optimise thumbnail image and clone original image property.

#### Example

Let's say we have a product which has a name, an image and thumbnail properties.

```csharp
using MSharp;

namespace Domain
{
    public class Product : EntityType
    {
        public Product()
        {
            String("Name").Mandatory();
            SecureImage("Photo").Mandatory().ValidExtensions("png,jpg");
            SecureImage("Thumbnail").OptimizationQuality(70).Width(100).Height(50);
        }
    }
}

```

As you can see, we have used `.OptimizationQuality(70).Width(100).Height(50)` respectively in order to generate a thumbnail with the specific size and quality. But this thumbnail property should be set automatically when a new product got save or edited, so we add a partial class and override `OnValidating()` method:

```csharp

using System;
using System.Threading.Tasks;

namespace Domain
{
    public partial class Product
    {
        protected override Task OnValidating(EventArgs e)
        {
            Thumbnail = this.Photo.Clone();

            return base.OnValidating(e);
        }
    }
}

```

We have added this class in the **Domain** project, under logic folder and we have cloned photo property on validating entity. Now we can use `Thumbnail` property everywhere we want and M# will handle all required action to generate a thumbnail image.