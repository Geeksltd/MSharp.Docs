# Page Settings

This lesson talks about page level settings in M#. In this lesson we will see how we can utilise page settings to control content and the look and feel of a page. Page settings are created and managed in M# **Project.cs** that is located in **#Model** project.

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

### Implementing Page Settings

By default M# defaine three default key for page setting:
- LeftMenu
- SubMenu
- TopMenu

`TopMenu` and `LeftMenu` page settings requires **Menu Module** name in camel case without any spaces.

```C#
using MSharp;

namespace Admin
{
    public class SettingsPage : SubPage<AdminPage>
    {
        public SettingsPage()
        {
            Set(PageSettings.LeftMenu, "AdminSettingsMenu");
            
            OnStart(x => x.Go<Settings.GeneralPage>().RunServerSide());
        }
    }
}
```

In the code above, for `SettingsPage` class we have used `Set()` method to set its `PageSettings.LeftMenu` value with `AdminSettingsMenu`. `AdminSettingsMenu` is a `MenuModule` that is created under **-Menus** folder of **#UI** project.