# Adding image/icon column

If your entity contains a Blob of type image you have two options for displaying the image on the generated Html table. The first approach is to use the Column method which according to the Blob type either generates an image tag or download link. Take the following entity for example

```csharp
using MSharp;

namespace Domain
{
    class Slide : EntityType
    {
        public Slide()
        {
            String("Title").Mandatory();
            String("Description").Mandatory();
            String("Link Url").Mandatory();
            String("Link Text").Mandatory();
            Int("Display Order").Mandatory();

            OpenImage("Image");
        }
    }
}

```
We can create the following List module, which only displays the image

```csharp
using Admin;
using Domain;
using Microsoft.EntityFrameworkCore.Internal;
using MSharp;
using System.Drawing;

namespace Modules
{
    class SlideTbl : ListModule<Domain.Slide>
    {
        public SlideTbl()
        {
            HeaderText("Slides");
            
            Search(GeneralSearch.AllFields).Label("Find:");
            SearchButton("Search").OnClick(x => x.Reload());
            
            Column(x => x.Title);
            Column(x => x.Description);
            Column(x => x.LinkUrl);
            Column(x => x.LinkText);
            Column(x => x.DisplayOrder);

            // this column only generates an img tag
            Column(x => x.Image);

        }
    }
}

```

Now if we need to configure the column or perhaps add some workflow to the click event of the column, we must use the ImageColumn method like below:

```csharp
using Admin;
using Domain;
using Microsoft.EntityFrameworkCore.Internal;
using MSharp;
using System.Drawing;

namespace Modules
{
    class SlideTbl : ListModule<Domain.Slide>
    {
        public SlideTbl()
        {
            HeaderText("Slides");
            
            Search(GeneralSearch.AllFields).Label("Find:");
            SearchButton("Search").OnClick(x => x.Reload());
            
            Column(x => x.Title);
            Column(x => x.Description);
            Column(x => x.LinkUrl);
            Column(x => x.LinkText);
            Column(x => x.DisplayOrder);

            //Column(x => x.Image);

            ImageColumn("Image")
                // Change column header
                .HeaderText("Background Image")
                // The image address to display in the table
                .ImageUrl("c#:item.Image.Url()")
                .Tooltip("Download")
                // on click workflow
                .OnClick(x => x.Go("c#:item.Image.Url()"));
        }
    }
}

```