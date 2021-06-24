# Mark-up Customisation

## Problem

MSharp has many built in methods to add CSS classes but sometimes you need to alter the underlying html structure.

## Implementation

There are several Markup methods to allow you to fully customise your view.

- `Markup()` – Gives you full control over where the elements in the object view will go:

 ```csharp
    Markup(@"
        <div>
            [#BUTTONS(SoftwareDevelopment)#] by [#BUTTONS(Geeks)#]
            &copy; @LocalTime.Now.Year. All rights reserved.
        </div>");

    Link("Geeks")
        .OnClick(x => x.Go(DEVELOPER, OpenIn.NewBrowserWindow));

    Link("Software development")
        .CssClass("plain-text")
        .OnClick(x => x.Go(DEVELOPER, OpenIn.NewBrowserWindow));
```

Elements can be referenced within the markup using placeholders, `[# #]`. For example, here where there are 2 buttons/links. The buttons have been differentiated by their property names.

Using `@` makes this a verbatim string literal that doesn’t require escaping of most special characters

- `MarkupWrapper()` – Add markup around the Module, the module itself is referenced using [#MODULE#]

```csharp
.MarkupWrapper("<div class='extra-div'>[#MODULE#]</div>");
```

- `MarkupTemplate()` – can be used to apply markup to a page, especially if there are multiple modules. Individual modules can be referred to using `[#1#]`, `[#2#]` etc.

- List Modules have additional markup methods to allow customisation of header, footer and data rows.

Care must be taken to ensure all tags are properly closed, this can often be checked within the cshtml file.
