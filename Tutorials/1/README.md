# App 1 - Tutorial
In this tutorial you will learn the following M# concepts.

- Entity Type Creation
- Association
- Page
- Navigation
- Button
- List Module
- Form Module
- Menu 


## Requirements :
We are going to implement Contact Managment System that you can see all available contacts and simpley do *CRUD* operation on each one of them. here are pictures of requirments :

![Contact List](ContactList.PNG "Contact List")
![Contact Form](ContactAddEdit.PNG "Contact Form")

By using M# framework you have the power of creating this application 4time faster than usual applicatoin development process, so lets see how we can acheive this.

## M# Structure :
![Structure of an M#](https://github.com/Geeksltd/MSharp.Docs/blob/master/Structure/DevModel.JPG "Structure of an M#")
As you can see, you as a devloper should interact to these projects. if you are not familier with this structure please look at [Structure of an M# solution](https://github.com/Geeksltd/MSharp.Docs/blob/master/Structure/README.md).
our development steps are :
1. Create required entity class in **@Model** project.
2. Generate created class in former step into **Domain** project.
3. Create and develop required pages based on generated classes in **@UI** project.

## Knowing Entities and Implementation :
In our example we have *Contact* and *Category* entity that have one to many relationship between *Contact* and *Category*. Our first step is to create *Contact* and *Category* classes.

### Adding Entities:
For adding new entity, right click on **@Model** project and add required C# class. We are going to create two entity, *Category* and *Contact* .

![Model Overview](https://github.com/Geeksltd/MSharp.Docs/blob/master/Tutorials/1/Model-Overview.PNG "Model Overview")

In M# the first thing a developer needs to do is to build a concrete business domain model, which consists of entities often referred to as business objects.
```C#
public class Category : EntityType
    {
        public Category()
        {
            String("Name").Mandatory();
        }
    }
```

```C#
public class Contact : EntityType
    {
        public Contact()
        {
            Associate<Category>("Category").Mandatory();

            String("First name").Mandatory();

            String("Last name").Mandatory();

            String("Tel").Mandatory();

            String("Email").Mandatory().Accepts(TextPattern.EmailAddress);
        }
    }
```

Every entity in M# should inherit from **EntityType** base class, this special class that instruct M# how to deal with entity. as you can see we have created an association between *Category* and *Contac*t entity and implement their properties. all properties are mandatory and for email property we have specified special validation that check email address format. 
after creating all entities, we are going to build our model. build your model by right click on **@Model** project and selecting **Build** from context menu. this step generate related C# class in **Domain** project that consist of all related code for generating and persisting data to data base. now it's time to build this project too, right click on **Domain** project and select **Build**. our final step start from here, **@UI** project deal with user interface and generate all required stuff that user interact with it. in **@UI** project we have three main step to do :
1. Add Pages
2. Config Menu
3. Add Modules To Pages

## Developing UI
In our example, we have a contact page that list our contacts and another page ro adding and editing each contact.

### Creating Contact Pages
Until now, we have done these steps :
1. Created our entities in **@Model** project and build the project in visual studio
2. Then build **Domain** project in visual studio.
Now it's time to create our first page. here we have to page, one that is responsible for showing contacts list and the other for adding and editing contact, these two page can have some property in commen, so first we create a parent page and then inherit other required page according to our example.
![UI Overview](https://github.com/Geeksltd/MSharp.Docs/blob/master/Tutorials/1/UI-Overview.PNG "UI Overview")
```C#
public class ContactPage : RootPage
{
    public ContactPage()
    {
        Add<MainMenu>();

        OnStart(x => x.Go<ContactsPage>().RunServerSide());
    }
}
```
this  is our root class that inherit from **RootPage** class, **RootPage** is a special class that tell M# framework how to deal with page. in **ContactPage.cs** I have mentioned that by the runing this page it should navigate to **ContactsPage.cs** that list all of my Contacts. so our next step is to create **ContactsPage.cs**

#### Creating Contact List Page & Contact List Module

```C#
public class ContactsPage : SubPage<ContactPage>
    {
        public ContactsPage()
        {
            Layout(Layouts.FrontEnd);

            Add<ContactsList>();
        }
    }
```
this class inherit from *ContactPage* and include Layout and Modules. with *Layout(Layouts.FrontEnd)* method I have specified page layout and by calling *Add\<ContactList>()* I told M# that this page should show ContactList module. implementation of **ContactList.cs** class is like this :
```C#
public class ContactsList : ListModule<Domain.Contact>
    {
        public ContactsList()
        {
            Column(x => x.Category);

            Column(x => x.FirstName);

            Column(x => x.LastName);

            Column(x => x.Tel).LabelText("Telephone");

            Column(x => x.Email);

            ButtonColumn("Edit").HeaderText("Actions").GridColumnCssClass("actions").Icon(FA.Edit)
                .OnClick(x => x.Go<EnterPage>()
                .Send("item", "item.ID").SendReturnUrl(false));

            ButtonColumn("Delete").HeaderText("Actions")
                .GridColumnCssClass("actions")
                .ConfirmQuestion("Are you sure you want to delete this Contact?")
                .CssClass("btn-danger")
                .Icon(FA.Remove)
                .OnClick(x =>
                {
                    x.DeleteItem();
                    x.RefreshPage();
                });

            Button("Add Contact")
                .Icon(FA.Plus)
                .OnClick(x => x.Go<EnterPage>().SendReturnUrl(false));
        }
    }
```
in this class we have include our needed column according to Visual Spec and add *Edit,Delete* and *Add Contact* buttons with there navigation instruction. you should notice that we have inherit from **ListModule** class, this class is special class that tell M# framework that how to generate code for showing this class.

#### Creating Contact Form Page & Contact Form Module
After creating contact list its time to create contact form page that is responsible for add or edit operation. we continue or work by creating contact form page in **@UI** project
```C#
public class EnterPage : SubPage<ContactsPage>
    {
        public EnterPage()
        {
            Layout(Layouts.FrontEnd);

            Add<ContactForm>();
        }
    }
```
As you can see, this class inherit from Contacts page and it instruct M# framework that this class is responsible for showing contact form module.
```C#
public class ContactForm : FormModule<Domain.Contact>
    {
        public ContactForm()
        {
            HeaderText("Contact Details");

            Field(x => x.Category).Control(ControlType.DropdownList);
            Field(x => x.FirstName).Control(ControlType.Textbox).Mandatory();
            Field(x => x.LastName).Control(ControlType.Textbox);
            Field(x => x.Email).Control(ControlType.Textbox);
            Field(x => x.Tel).Control(ControlType.Textbox).Label("Telephone");

            Button("Cancel").CausesValidation(false)
                .OnClick(x => x.ReturnToPreviousPage());

            Button("Save").IsDefault().Icon(FA.Check)
                .OnClick(x =>
                {
                    x.SaveInDatabase();
                    x.GentleMessage("Saved successfully.");
                    x.ReturnToPreviousPage();
                });
        }
    }
```
Another important module is form module that deal with add or edit entity. this class inherit from **FormModule** class that tell M# framework how to deal with this class. this special class tell M# that it should generate form page that is responsible for Add or Edit entity.

### Adding Contact List Page to Menu
our last step is to include *contact list page* in main menu, for doing this open **MainMenu.cs** class and add *ContactPage* class here as menu item.
```C#
public class MainMenu : MenuModule
    {
        public MainMenu()
        {
            AjaxRedirect().IsViewComponent().UlCssClass("nav navbar-nav dropped-submenu");

            Item("Login").Icon(FA.UnlockAlt).VisibleIf(AppRole.Anonymous)
                .OnClick(x => x.Go<LoginPage>());

            Item("Settings").Icon(FA.Cog).VisibleIf(AppRole.Administrator)
                .OnClick(x => x.Go<SettingsPage>());

            Item("Contacts").Icon(FA.Cog)
                .OnClick(x => x.Go<ContactPage>());
        }
    }
```
By adding *ContactPage* class as menu item here, we tell M# framework that by clicking on Contacts link, it should navigate user to *ContactPage* that this page show list of all contacts in our database. 
now its time to build **@UI** project, this project generated related files in **WebSite** project, set this project as you default *StartUp* project and set your *connection string* in **appsetting.json** file and then hit F5 to see M# magic. your project is ready to use in short time.