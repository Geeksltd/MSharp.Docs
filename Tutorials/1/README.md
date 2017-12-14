# App 1 - Tutorial
In this lesson you will learn the following M# concepts.

- Entity Type Creation
- Association
- Page
- Navigation
- Button
- List Module
- Form Module
- Menu 


## Wireframe :
[http://design.visualspec.co.uk/?p=MSharp.Tutorial.1&user=1&S1_2=3](http://design.visualspec.co.uk/?p=MSharp.Tutorial.1&user=1&S1_2=3)

## Adding New Entity :
For adding new entity, right click on **@Model** project and add C# class. as you have saw in Visual Spec, we are going to create two entity, *Category* and *Contact* .

![Overview diagram](Model-Overview.png "M# Overview")

In M# the first thing a developer needs to do is to build a concrete business domain model, which consists of entities often referred to as business objects. in our example we are going to create *Category* and *Contact* entity like this :
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

every entity in M# should inherit from **EntityType** base class, this special class that instruct M# how to deal with entity. as you can see we have created an association between *Category* and *Contac*t entity and implement their properties. all properties are mandatory and for email property we have specified special validation that check email address format. 
after creating all entities, we are going to build our model. build your model by right click on **@Model** project and selecting **Build** from context menu. this step generate related C# class in **Domain** project that consist of all related code for generating and persisting data to data base. now it's time to build this project too, right click on **Domain** project and select **Build**. our final step start from here, **@UI** project deal with user interface and generate all required stuff that user interact with it. in **@UI** project we have three main step to do :
1. Add Pages
2. Config Menu
3. Add Modules To Pages

#### Adding Page
In our example, we have contact page that hold list and contact form. as you can see, I have created root page with the name of **ContactPage.cs** that act like holder for **EnterPage.cs** and **ContactsPage.cs** and these two pages inherit from their parent.

![Overview diagram](UI-Overview.png "M# Overview")

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
another important Module is form module that deal with add or edit entity:
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
this class inherit from **FormModule** class that tell M# framework how to deal with this class. this special class tell M# that it should generate form page that is responsible for Add or Edit entity.
our last step is to include *contact page* in main menu, for doing this open **MainMenu.cs** class and add *ContactPage* class here as menu item.
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
by adding *ContactPage* class as menu item here, we tell M# framework that by clicking on Contacts link, it should navigate user to *ContactPage* that this page show list of all contacts in our database. 
now its time to build **@UI** project, this project generated related files in **WebSite** project, set this project as you default *StartUp* project and set your *connection string* in **appsetting.json** file and then hit F5 to see M# magic. your project is ready to use in short time.