# Click action on an image

## Problem

In general, it is great to have common standards in the UI to not force users to learn lots of design language but at the same time intuitiveness is important too.
In some situations, instead of the usual button/link , we want to make the image of a data set clickable for showing more details or any other purpose that usually a link or a button is used.
In this topic we describe how to make an image clickable and how to tell it what to do in M#

## Implementation

The `OnClick()` fluent method can be used on an `ImageColumn` to to make it clickable and also tell it what to do in the lambda that the OnClick accepts as parameter.

#### Example

Let's say we have a list of products which whenever you click on one of them, you'll navigate to the view page for products and view the product in a more detailed manner.

the list module will be written like this

```csharp
using MSharp;

namespace Modules
{
    public class ProductsList : ListModule<Domain.Product>
    {
        public ProductsList()
        {
            Column(x => x.ProductName);
            ImageColumn("Photo").ImageUrl("@item.Photo").OnClick(x =>
            {
            x.Go<Product.ViewPage>().Send("item", "item.ID"));

        });
        }
    }
}
```

As you can see we used `OnClick()` on a `ImageColumn` just like what we do with a button.
Then we tell M# to move to view page and then send the `ID of the current item to it as well.
In this way we made our buttons interactive.
