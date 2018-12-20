# Image Optimization

## Problem

One of the most common file types which are usually stored in applications are images.
Images consume lots of space and if not careful, can cause your application to use much RAM and disk space on the server and load slowly on a client's device.

When you design a website, the images can be optimized by the artist working on them or one of the developers but when you are accepting images from users, you need to only accept images with certain sizes and qualities and also optimize images after receiving them.
Since M# always thinks of your needs, it has methods to optimize images and deal with this issue.
Using them is as easy as it possibly could be and we will take a look at the feature here.

## implementation

When you define a `SecureImage` property in an entity, you can use the following methods on the property to optimize it.

- `Width()` specifies the maximum width of the image, if the image's width is larger than this, the image's size is reduced so the width is at max this value
- `Height()` Specifies the max height of the image. If the image has a height larger than this, it is resized to a smaller size so the height is at max this value.
- `OptimizationQuality()` Sets the quality of the image after optimization. The accepted range is between 0 and 100. The higher the value, the higher the image quality will be but it will have a bigger size as well.
- `AutoOptimize()` If you call this method, the image will be optimized with the default setings of 800x600 and 70% optimization quality.

If you don't call any of these, the image will not be optimized at all.

#### Example

Let's define a product entity which has an image and optimize the quality of its image so it doesn't take much space.

```csharp
using MSharp;


namespace Domain
{
    public class Product : EntityType
    {
        public Product()
        {
            String("Product Name").Mandatory();
            SecureImage("Photo").Mandatory().OptimizationQuality(75).Width(400).Height(400);
        }
    }
}
```

The optimization quality is set to 75%, max width & height is 400.

#### Generated Code

Let's take a look at the generated code

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
                    value.OptimizeImage(400, 400, 75);
                }

                photo = value.Attach(this, "Photo");
            }
        }
	...

}
```

In the setter of the `Photo` property, the `OptimizeImage()` method is called which optimizes the imagebased on the specified settings before we actually store it in the entity.

## Remarks

If you are not sure if your settings for optimizations are good enough or not, test the settings instead of guessing.
You should find a good balance between size and acceptable quality which sometimes is art more than science.