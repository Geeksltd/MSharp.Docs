# Master Page

Master pages in web development are used to develop a template, which is inherited by webpages to follow the same design theme and to share the common and global functionality.

In M# master pages are managed in **project.cs** file in **#Model** project as shown below:

```C#
using MSharp;

namespace App
{
    public class Project : MSharp.Project
    {
        public Project()
        {
            SqlDialect(MSharp.SqlDialect.MSSQL);

            Name("AppSample").SolutionFile("AppSample.sln");

            Role("Local.Request");
            Role("Anonymous");
            Role("Admin").SkipQueryStringSecurity();

            Layout("Front end").AjaxRedirect().Default().VirtualPath("~/Views/Layouts/FrontEnd.cshtml");
            Layout("Blank").AjaxRedirect().VirtualPath("~/Views/Layouts/Blank.cshtml");
            Layout("Front end Modal").Modal().VirtualPath("~/Views/Layouts/FrontEnd.Modal.cshtml");

            PageSetting("LeftMenu");
            PageSetting("SubMenu");
            PageSetting("TopMenu");

            AutoTask("Clean old temp uploads").Every(10, TimeUnit.Minute)
                .Run("await Olive.Mvc.FileUploadService.DeleteTempFiles(olderThan: 1.Hours());");
        }
    }
}
```

You can add more master pages as required by using `Layout()` method. M# creates three types of master pages when a new project is created in M#. 

- **Front end** layout is used to develop **Standard** pages
- **Front end Modal** layout is used to develop **Modal / popup** pages which are discussed in another lesson of this chapter.
- **Blank** layout is used to develop a page with a clean stype

You can choose one of the these master pages when you created a `SubPage` as shown in the code below:

```C#
using MSharp;

namespace SampleEntity
{
    class EnterPage : SubPage<SampleEntityPage>
    {
        public EnterPage()
        {
            Layout(Layouts.FrontEnd);

            // Add related modules
        }
    }
}
```

For more information on creating pages please read [M# Concepts](https://github.com/Geeksltd/MSharp.Docs/blob/master/Basics/Concepts.md).