# Custom Data Source

## Problem

When using a View module for an entity, the default data source is the ID of the entity that gets passed through from a previous page.

An example of this is when clicking on the Name of an Employee from a list, which then redirects you to view that Employee's details based on its ID.

In other cases, however, you might want to use a custom data source instead of the default used.

For example, you have a single View module that is used for showing any type of Content Block, such as Privacy Policy or Terms & Conditions. The module also uses custom markup and needs to show the correct Content Block, based on a provided Key.

## Implementation

With MSharp, you can change the data source used for a View module by using `DataSource()`.

```csharp
public class ContentBlockView : ViewModule<Domain.ContentBlock>
{
    public ContentBlockView()
    {
        DataSource("await ContentBlock.FindByKey(info.Key)");
        
        Markup("@info.Output.Raw()");

        ViewModelProperty<string>("Key");
        ViewModelProperty<string>("Output")
            .Getter(@"if (Item == null) return ""No content found for key: '"" + Key + ""'"";
            return Item.GetMarkup();");
    }
}
```
