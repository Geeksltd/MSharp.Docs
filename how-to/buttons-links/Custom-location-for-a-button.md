# Custom location for a button

By Default Links and Buttons are wrapped in a div element with the “buttons-row” class, which will be rendered at the bottom of the module, you can render them at the top of the module by calling ButtonsLocation(string value) method and set its input to “Top” or “Bottom”. Like below:

```csharp

using MSharp;

namespace Modules
{
    class SlideFrm : FormModule<Domain.Slide>
    {
        public SlideFrm()
        {
            HeaderText("Slide details");
            
            Field(x => x.Title);
            Field(x => x.Description);
            Field(x => x.LinkUrl);
            Field(x => x.LinkText);
            Field(x => x.DisplayOrder);
            Field(x => x.Image);

            ButtonsLocation("Top");

            Link("Cancel").OnClick(x => x.Go<Admin.SlidesPage>());
            
            Button("Save").IsDefault().Icon(FA.Check)
            .OnClick(x =>
            {
                x.SaveInDatabase();
                x.GentleMessage("Saved successfully.");
                x.Go<Admin.SlidesPage>();
            });
        }
    }
}


```

You can also change the wrapping markup of each button in order to position them by using custom css classes.

```csharp
using MSharp;

namespace Modules
{
    class SlideFrm : FormModule<Domain.Slide>
    {
        public SlideFrm()
        {
            HeaderText("Slide details");
            
            Field(x => x.Title);
            Field(x => x.Description);
            Field(x => x.LinkUrl);
            Field(x => x.LinkText);
            Field(x => x.DisplayOrder);
            Field(x => x.Image);

            ButtonsLocation("Bottom");

            Button("Cancel").OnClick(x => x.Go<Admin.SlidesPage>());
            
            Button("Save").IsDefault().Icon(FA.Check)
            .OnClick(x =>
            {
                x.SaveInDatabase();
                x.GentleMessage("Saved successfully.");
                x.Go<Admin.SlidesPage>();
            })
            .MarkupTemplate(@"
                <div class='custom-button-template'>
                    [#Button#]
                </div>
            ");

            
        }
    }
}

```