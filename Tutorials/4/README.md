# M# Tutorial - Episode 4: Search

In this tutorial you will learn:

- Property search element
- All fields search element
- Custom Label for form / search elements

## Requirements

In this tutorial, we are going to implement an asset management system that lets users to do CRUD operations on assets and owners, and let them to search and find assets and related owners easily.
Here are the sketches for list and model.

### Asset Types

![Asset Types List](AssetType.PNG "Asset Types List")

![Asset Type Add/Edit](AssetTypeAddEdit.PNG "Asset Type Add/Edit")

For asset types, there are just CRUD operations.

### Owner

![Owner](Owner.PNG "Owner")

![Owner Add/Edit](OwnerAddEdit.PNG "Owner Add/Edit")

For owners, there are just simple CRUD operations, same as asset types.

### Assets

![Assets](Assets.PNG "Assets")

![Asset Add/Edit](AssetAddEdit.PNG "Asset Add/Edit")

As you can see, In the assets list there are filter and search  columns, and in editing mode, the default label should be changed to custom one.

## Implementation: Entities

From requirements, three entities can be identified; "Asset Type", "Owner" and "Assets". In "Asset" entity, there are two One-to-Many relationships. One with the owner and the other one with the asset type.
After understanding requirements and identifying its related properties and their relationships, it's time to create them. Now let's create the corresponding classes in the *#Model* project.

Navigate to the **#Model** project and create a **Domain** folder, *right click > Add > M#* and then create three entities named **AssetType**, **Owner** and **Asset** using the following code snippets:

```csharp
using MSharp;

namespace Domain
{
    public class AssetType : EntityType
    {
        public AssetType()
        {
            Name("Asset Type");

            String("Name");
        }
    }
}
```

```csharp
using MSharp;

namespace Domain
{
    public class Owner : EntityType
    {
        public Owner()
        {
            Name("Owner");

            String("First name");

            String("Last name");

            ToStringExpression("FirstName + ' ' + LastName");
        }
    }
}
```

In owner class, a new M# method have been used. It's `ToStringExpression()`, as its name applies, this method is used for changing default M# `.ToString()` behavior and here we tell M# framework that it should render *First Name + Last Name* to show entity.

```csharp
using MSharp;

namespace Domain
{
    public class Asset : EntityType
    {
        public Asset()
        {
            Name("Asset");

            String("Code");

            String("Name");

            Associate<AssetType>("Type");

            Money("Cost");

            Associate<Owner>("Owner");
        }
    }
}
```

As you can see, there are two relations, one with *AssetType* and the other one with *Owner* class. For *Cost* property, we have used `Money()` methods that tell M# framework how to behave and render this property.
Now it's time to feed our two entity types to M# code generator. In solution explorer, right click the *#Model* project and select *Build* to build the *Domain* project, in order to make sure everything's fine.

## Implementation: UI

According to the requirement, we need these pages:

- Asset Types List
  - Add / Edit Asset Types
- Owners List
  - Add / Edit Owner
- Assets List (with search and filter)
  - Add / Edit Asset

So, there are three root pages that hold our list modules and six sub pages that are related to add or edit operation.

### Creating Asset Type Pages

Navigate to *Pages* folder of the *#UI* project; Then add a class named *Asset Type* or you can use M# context menu to add *Asset Type* root page:

```csharp
using MSharp;

public class AssetTypePage : RootPage
{
    public AssetTypePage()
    {
        Add<Modules.AssetTypesList>();
    }
}
```

As you can see, we have added `Add<Modules.ProjectsList>();`. We're going to create this class soon, but for now let's skip it for a while. In the *Pages* folder create a new folder named *AssetTypes* then make a class named *EnterPage* class in *AssetTypes* folder like below:

```csharp
using MSharp;

namespace AssetTypes
{
    class EnterPage : SubPage<AssetTypePage>
    {
        public EnterPage()
        {
            Layout(Layouts.FrontEnd);

            Add<Modules.AssetTypeForm>();
        }
    }
}
```

As you can see, this class holds asset type form module.

### Creating required module of Asset Type Pages

Add a folder with the name of *AssetType* under the *Modules* folder of the *#UI* project and add a class with the name of *AssetTypesList*. It can be done easier by using the M# context menu like below:

![M# Context Menu](UsingContextMenu.PNG "M# Context Menu")

```csharp
using MSharp;

namespace Modules
{
    public class AssetTypesList : ListModule<Domain.AssetType>
    {
        public AssetTypesList()
        {
            HeaderText("Asset Types");

            Column(x => x.Name);

            ButtonColumn("Edit").Icon(FA.Edit)
                .OnClick(x => x.Go<AssetTypes.EnterPage>()
                .Send("item", "item.ID")
                .SendReturnUrl());

            ButtonColumn("Delete").Icon(FA.Remove)
                .OnClick(x =>
                {
                    x.DeleteItem();
                    x.Reload();
                });

            Button("New Asset Types").Icon(FA.Plus)
                .OnClick(x => x.Go<AssetTypes.EnterPage>()
                .SendReturnUrl());
        }
    }
}
```

In this class, a list of asset types are shown according to the requirements. Also a route for adding, editing and removing items.

Add *AssetTypeForm* class by using the M# context menu under the *AssetType* folder of the *Modules* like below:

```csharp
using MSharp;

namespace Modules
{
    public class AssetTypeForm : FormModule<Domain.AssetType>
    {
        public AssetTypeForm()
        {
            HeaderText("Asset Types details");

            Field(x => x.Name);

            Button("Cancel").OnClick(x => x.ReturnToPreviousPage());

            Button("Save").IsDefault().Icon(FA.Check)
            .OnClick(x =>
            {
                x.SaveInDatabase();
                x.GentleMessage("Saved successfully.");
                x.ReturnToPreviousPage();
            });
        }
    }
}
```

This class is responsible for generating related forms for adding and editing entity. After creating these modules, add them to *AssetType.cs* class that is our root page, and *Enter.cs* class under *AssetTypes* folder if you have let them empty in previous sections.

### Creating Owner Pages

Go to *Pages* folder of *#UI* project then create a class named *Owner*. Also you can use M# context menu to add the *Owner* root page:

```csharp
using MSharp;

public class OwnerPage : RootPage
{
    public OwnerPage()
    {
        Add<Modules.OwnersList>();
    }
}
```

In this class we added *OwnerList* module which is responsible for showing all owners. Let's continue with creating an *Enter* class that is responsible for adding and editing owners. Create a new folder with the name of *Owners* under the *Pages* folder in *#UI* project, then add an *EnterPage* class like below:

```csharp
using MSharp;

namespace Owners
{
    class EnterPage : SubPage<OwnerPage>
    {
        public EnterPage()
        {
            Layout(Layouts.FrontEnd);

            Add<Modules.OwnerForm>();
        }
    }
}
```

In this class we added *OwnerForm* module which tells M# framework how to generate related codes for this class.

### Creating required module of Owner Pages

Now it's time to create related *Modules*. Two modules are needed for owner entity; **ListModule** and **FormModule**. Create a new folder named *Owner* under the *Modules* folder of *#UI* project,then add a *form module* and a *list module* using M# context menu:

```csharp
using MSharp;

namespace Modules
{
    public class OwnerForm : FormModule<Domain.Owner>
    {
        public OwnerForm()
        {
            HeaderText("Owner details");

            Field(x => x.FirstName);
            Field(x => x.LastName);

            Button("Cancel").OnClick(x => x.ReturnToPreviousPage());

            Button("Save").IsDefault().Icon(FA.Check)
            .OnClick(x =>
            {
                x.SaveInDatabase();
                x.GentleMessage("Saved successfully.");
                x.ReturnToPreviousPage();
            });
        }
    }
}
```

```csharp
using MSharp;

namespace Modules
{
    public class OwnersList : ListModule<Domain.Owner>
    {
        public OwnersList()
        {
            HeaderText("Owners");

            Column(x => x.FirstName);
            Column(x => x.LastName);

            ButtonColumn("Edit").Icon(FA.Edit)
                .OnClick(x => x.Go<Owners.EnterPage>()
                .Send("item", "item.ID")
                .SendReturnUrl());

            ButtonColumn("Delete").Icon(FA.Remove)
                .OnClick(x =>
                {
                    x.DeleteItem();
                    x.Reload();
                });

            Button("New Owner").Icon(FA.Plus)
                .OnClick(x => x.Go<Owners.EnterPage>()
                .SendReturnUrl());
        }
    }
}
```

These two classes are responsible for CRUD (Create, Read, Update, Delete) operations.

### Creating Asset Pages

Our last step is to create related pages for *Asset* entity. Go to *Pages* folder of *#UI* and use M# context menu to add an *Asset* root page:

```csharp
using MSharp;

public class AssetPage : RootPage
{
    public AssetPage()
    {
        Add<Modules.AssetsList>();
    }
}
```

In this class *AssetsList* module is added, which is responsible for showing all assets. Now let's continue with creating an *Enter* class for adding and editing assets. Create a new folder with the name of *Assets* under the *Pages* folder of *#UI* project and add an *Enter* sub page using M# context menu:

```csharp
using MSharp;

namespace Assets
{
    class EnterPage : SubPage<AssetPage>
    {
        public EnterPage()
        {
            Layout(Layouts.FrontEnd);

            Add<Modules.AssetForm>();
        }
    }
}
```

In this class we added *AssetForm* module that tells M# framework how to generate related form code for this class.

Add another sub page, named "View":

```csharp
using MSharp;

namespace Assets
{
    class ViewPage : SubPage<AssetPage>
    {
        public ViewPage()
        {
            Layout(Layouts.FrontEnd);

            Add<Modules.AssetView>();
        }
    }
}
```

This class is responsible for the view-only purposes and we have added *AssetView* module.

### Creating required module of Asset Pages

Now, let's continue our work by creating related *Modules*. Three modules are needed for asset entity; **ListModule**, **FormModule** and **ViewModule**. Create a new folder with the name of *Asset* under the *Modules* folder of *#UI* project, then add the following form, list and view classes using M# context menu:

```csharp
using MSharp;

namespace Modules
{
    public class AssetForm : FormModule<Domain.Asset>
    {
        public AssetForm()
        {
            HeaderText("Asset details");

            Field(x => x.Code);
            Field(x => x.Name);
            Field(x => x.Type).Label("Asset type");
            Field(x => x.Cost);
            Field(x => x.Owner).Label("Who is currently holding it?");

            Button("Cancel").OnClick(x => x.ReturnToPreviousPage());

            Button("Save").IsDefault().Icon(FA.Check)
            .OnClick(x =>
            {
                x.SaveInDatabase();
                x.GentleMessage("Saved successfully.");
                x.ReturnToPreviousPage();
            });
        }
    }
}
```

In this class, the `.Label()` method is used. This method helps you to write your custom label for the property and we have added custom text according to the requirement.

```csharp
using MSharp;

namespace Modules
{
    public class AssetsList : ListModule<Domain.Asset>
    {
        public AssetsList()
        {
            HeaderText("Assets");

            Search(x => x.Type).Label("Type:");

            Search(GeneralSearch.AllFields).Label("Find:");

            SearchButton("Search");

            ButtonColumn("View").HeaderText("View").Icon(FA.SearchPlus)
                .OnClick(x => x.Go<Assets.ViewPage>().Send("item", "item.ID").SendReturnUrl());

            Column(x => x.Code);
            Column(x => x.Name);
            Column(x => x.Type).LabelText("Asset type");
            Column(x => x.Cost);
            Column(x => x.Owner);

            ButtonColumn("Edit").Icon(FA.Edit)
                .OnClick(x => x.Go<Assets.EnterPage>()
                .Send("item", "item.ID")
                .SendReturnUrl());

            ButtonColumn("Delete").Icon(FA.Remove)
                .OnClick(x =>
                {
                    x.DeleteItem();
                    x.Reload();
                });

            Button("New Asset").Icon(FA.Plus)
                .OnClick(x => x.Go<Assets.EnterPage>()
                .SendReturnUrl());
        }
    }
}
```

In this class some new M# methods have been used. `Search()` method lets us to add new search and filter capacity. By using `Search(x => x.Type).Label("Type:");` we tell M# that we need a filter over *Type*  property with custom text "Type:". By using `Search(GeneralSearch.AllFields).Label("Find:");` we add search for all columns to our list module and we have added a search button with "Search" label that lets users search through entities.

```csharp
using MSharp;

namespace Modules
{
    public class AssetView : ViewModule<Domain.Asset>
    {
        public AssetView()
        {
            HeaderText("Asset details");

            Field(x => x.Code);
            Field(x => x.Name);
            Field(x => x.Type).LabelText("Asset type");
            Field(x => x.Cost);
            Field(x => x.Owner).LabelText("Held by");

            Button("Back").Icon(FA.ChevronLeft).OnClick(x => x.ReturnToPreviousPage());
        }
    }
}
```

This class just shows asset details and let the users go back to the previous page by clicking on "Back" button.

### Adding Pages to the Menu

Our last step is to add the root pages to the main menu:

```csharp
using MSharp;

namespace Modules
{
    public class MainMenu : MenuModule
    {
        public MainMenu()
        {
            AjaxRedirect().IsViewComponent().UlCssClass("nav navbar-nav dropped-submenu");

            Item("Login").Icon(FA.UnlockAlt).VisibleIf(AppRole.Anonymous)
                .OnClick(x => x.Go<LoginPage>());

            Item("Settings").Icon(FA.Cog).VisibleIf(AppRole.Administrator)
                .OnClick(x => x.Go<Admin.SettingsPage>());

            Item("Asset Types").Icon(FA.Navicon)
               .OnClick(x => x.Go<AssetTypePage>());

            Item("Owners").Icon(FA.Navicon)
               .OnClick(x => x.Go<OwnerPage>());

            Item("Assets List").Icon(FA.Navicon)
               .OnClick(x => x.Go<AssetPage>());
        }
    }
}
```

### Final Step

Build **#UI** project, set the **WebSite** project as your default *StartUp* project and configure your *connection string* in **appsetting.json** file and hit F5. Your project is ready to use.
