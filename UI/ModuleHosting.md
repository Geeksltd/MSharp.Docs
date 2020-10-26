# Module Hosting

In this lesson we will learn to host /add modules on the page and how we can define a layout for them. (For more information about modules or pages please read [M# Concepts](https://github.com/Geeksltd/MSharp.Docs/blob/master/Basics/Concepts.md)).

M# allows developers to host as many modules as required on page. You can add new or existing modules. M# provides a separate folder under **#UI** project name **Modules** where all the modules are hosted and managed. By default, M# renders the modules in the sequence they are hosted on the page, which can be changed by developer.

```csharp
using MSharp;

namespace Supplier
{
    class EnterPage : SubPage<SamplePage>
    {
        public EnterPage()
        {
            Layout(Layouts.AdminDefault);

            // Add modules here like this one:
            Add<Modules.SampleForm>();
        }
    }
}
```

For adding modules you should just use `Add<T>()` generic method and call related module class.