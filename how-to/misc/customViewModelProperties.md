# Custom ViewModel Properties

## Problem

You need to add another property to the ViewModel.

## Implementation

You can add new properties to the ViewModel by using `ViewModelProperty()`.

``` csharp
public ContentBlockView()
{
    IsViewComponent()
        .DataSource("await ContentBlock.FindByKey(info.Key)")
        .Markup("@info.Output.Raw()");


    ViewModelProperty<string>("Key").FromRequestParam("item");

    ViewModelProperty<string>("Output")
        .Getter(@"if (Item == null) return ""No content found for key: '"" + Key + ""'"";
                return Item.Body;");
}
```

This may be done for several reasons.

- You may need to add more information to the ViewModel. In this case a new property can be created from a query string. In the above example a ViewModel Property of type string has been created called "Key", the value has been taken from the query string “item”.

- You may wish to provide more abstraction. In this case the ViewModel property output has been created using a `Getter`. This allows the removal of repetitive or long code making the code easier to read.

These properties can then be called from methods in the module. The instance of ViewModel used in the controller is called info. So in this case Key can be accessed by using `info.Key` as seen above in `DataSource()`.

The properties the ViewModel has can be seen in the controller, generally at the bottom. This is useful if you are having difficulty giving properties unique names.
