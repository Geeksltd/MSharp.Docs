# Your Forth M# Application
In this tutorial you will learn:

 - Property search element
 - All fields search element
 - Custom Label for form / search elements

## Requirements
In this tutorial we are going to implement an asset management system that lets users to do CRUD operation on assets and owners and let them to search and find assets and related owners easily.
Here are the sketches for list and model.

### Asset Types:
![Asset Types List](AssetType.PNG "Asset Types List")

![Asset Type Add/Edit](AssetTypeAddEdit.PNG "Asset Type Add/Edit")

For asset types, we just have simple CRUD operation.

### Owner:
![Owner](Owner.PNG "Owner")

![Owner Add/Edit](OwnerAddEdit.PNG "Owner Add/Edit")

For owners, we just have simple CRUD operation, too.

### Assets:
![Assets](Assets.PNG "Assets")

![Asset Add/Edit](AssetAddEdit.PNG "Asset Add/Edit")

As you can see, In the assets list we have filter and search  columns, and in editing mode, we should change the default label to custom one.

## Implementation
From requirements, we can identify three entities, "Asset Type", "Owner" and "Assets". In asset entity, we have two One-to-Many relationships one with the owner and the other one with asset type.  
After understanding requirements and identifying its related entities and their relationships, it's time to create them. Now let's create the corresponding classes in the *#Model* project.

## Creating M# Entity Types
We start our work by creating related classes in a *#Model* project under *Domain* folder:

```C#
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

```C#
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
In owner class, we have used new M# method. It's **ToStringExpression()**, as its name applies, we use this method to change default M# *.ToString()* behavior and here we tell M# framework that it should render *First Name + Last Name* for showing entity.

```C#
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
As you can see, We have two relations, one with *AssetType* and the other one with *Owner* class. For *Cost* property, we have used *Money()* methods that tell M# framework how to behave and render this property.
Now it's time to feed our two entity types to the M# code generator. In solution explorer, right click the *#Model* project and select *Build* and then build the *Domain* project to make sure everything regarding it is fine.

## Developing UI
According to the requirement, we have these pages:

- Asset Types List
  - Add / Edit Asset Types
- Owners List
  - Add / Edit Owner
- Assets List (with search and filter)
  - Add / Edit Asset

So, we have three root pages that hold our list modules and 6 sub pages that are related to add or edit operation.

### Creating Asset Type Pages
Use M# context menu to add *Asset Type* root page:

```C#
using MSharp;

public class AssetTypePage : RootPage
{
    public AssetTypePage()
    {
        Add<Modules.AssetTypesList>();
    }
}
```
As you can see, we have added **Add\<Modules.ProjectsList>();**, we are going to create this class soon and for now just skip it and we continue our work be creating a *Enter* class like bellow:

```C#
using MSharp;

namespace AssetTypes
{
    class Enter : SubPage<AssetTypePage>
    {
        public Enter()
        {
            Layout(Layouts.FrontEnd);

            Add<Modules.AssetTypeForm>();
        }
    }
}
```
Create a new folder with the name of *AssetTypes* and then add the above class as a sub-page for *AssetTypePage*, this class holds asset type form module.

#### Creating Asset Types List Module
Add a folder with the name of *AssetType* under the *Modules* folder of the *#UI* project and add *AssetTypesList* by using the M# context menu like bellow:

![M# Context Menu](UsingContextMenu.PNG "M# Context Menu")

```C#
using MSharp;

namespace Modules
{
    public class AssetTypesList : ListModule<Domain.AssetType>
    {
        public AssetTypesList()
        {
            HeaderText("Asset Typeses");

            Column(x => x.Name);

            ButtonColumn("Edit").Icon(FA.Edit)
                .OnClick(x => x.Go<AssetTypes.Enter>()
                .Send("item", "item.ID")
                .SendReturnUrl());

            ButtonColumn("Delete").Icon(FA.Remove)
                .OnClick(x =>
                {
                    x.DeleteItem();
                    x.Reload();
                });

            Button("New Asset Types").Icon(FA.Plus)
                .OnClick(x => x.Go<AssetTypes.Enter>()
                .SendReturnUrl());
        }
    }
}
```
In this class we show a list of asset types according to the requirements and add a route for adding, editing and removing items.

#### Creating Asset Type Form Module
Add *AssetTypeForm* class by using the M# context menu under the *Modules* folder of the *#UI* project in *AssetType* like bellow:

```C#
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
This class has responsibility for generating related forms for adding and editing entity. After creating these modules, please add them to *AssetType.cs* class that is our root page and *Enter.cs* class under *AssetTypes* folder if you have let them empty in previous sections.

#### Creating Owner Pages
Comming soon...