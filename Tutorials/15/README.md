# M# Tutorial - Episode 15

In this tutorial you will learn:

- List column format (date and percentage, and number separator)
- Form element display expression
- Search element display expression 

## Requirements

In this tutorial, we are going to implement a website that manages countries and companies. Some elements of companies have specific formats and we will show country name in different ways.

### Countries


![Countries](Countries.PNG "Countries")
![Countries Add/Edit](CountryAdd.PNG "Countries Add/Edit")

As you can see, each country has a name and a code which is a simple abbreviation of the country name.


### Companies

![Companies](Companies.PNG "Companies")
![Company Add/Edit](CompanyAdd.PNG "Company Add/Edit")

 Every company will have a company name, a registration date with a specific format, market share which is percentage based, number of employees which is formatted with a thousand separator and a country. 
 When you are selecting a country in the Form of the company, instead of showing just the name of the country it should show the code and in the parenthesis the country name, but in the search element, we only show the code of the company.


## Implementation : Entities


Two entities can be identified, "Country" and "Company". After analyzing the requirements and identifying related properties, it's time to create them. Now let's create the corresponding classes in the **#Model** project.

Create a **Domain** folder and add these classes:

```C#
using MSharp;

namespace Domain
{
    public class Country : EntityType
    {
        public Country()
        {
            String("Name").Mandatory();

            String("Code").Mandatory();
        }
    }
}
```

```C#
using MSharp;

namespace Domain
{
    public class Company : EntityType
    {
        public Company()
        {
            String("Name").Mandatory();

            Date("Registration date").Mandatory();

            Decimal("Market share").IsPercentage().Scale(2).Min(0).Max(100).Mandatory();

            Int("Number of employees").Mandatory();

            Associate<Country>("Country").Mandatory();
        }
    }
}
```

In company class, a new M# method have been used. It's `IsPercentage()`, as its name applies, this method is used for showing percentage mark.

After adding these classes, build **#Model** and after that **Domain** project to make sure everything regarding it is fine.

## Implementation

As we can see in the requrements, we should develop these pages:

- Companies
  - Add company
-Countries
  - Add country

### Company Page

Go to **Pages** folder of **#UI**, right *click > Add > M#*  then create **Company** rootpage:

```C#
using MSharp;
public class CompanyPage : RootPage
{
    public CompanyPage()
    {
        Add<Modules.CompaniesList>();
    }
}
```

Now create a folder named **Country** under the **Pages** folder. Then add an **Enter** class here:

```C#
using MSharp;

namespace Company
{
    public class EnterPage : SubPage<CompanyPage>
    {
        public EnterPage()
        {
            Add<Modules.CompanyForm>();
        }
    }
}
```

#### Creating required module of Company Page

Navigate to **Modules** folder of **M#** project and create folder named **Company**. Then add a *Form module* named **CompanyForm** using M# context menu:

```C#
using MSharp;

namespace Modules
{
    public class CompanyForm : FormModule<Domain.Company>
    {
        public CompanyForm()
        {
            HeaderText("Company details");

            Field(x => x.Name);

            Field(x => x.RegistrationDate);

            Field(x => x.MarketShare);

            Field(x => x.NumberOfEmployees);

            Field(x => x.Country).DisplayExpression("item.Code + \"(\" + item.Name + \")\"");

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

As you can see, we use `DisplayExpression()` method to show the country name how we want.
Then add the **CompaniesList** module:

```C#
using MSharp;

namespace Modules
{
    public class CompaniesList : ListModule<Domain.Company>
    {
        public CompaniesList()
        {
            HeaderText("Companies");

            Search(c => c.Country).DisplayExpression("item.Code");

            SearchButton("Search");

            Column(x => x.Name).LabelText("Company name");

            Column(x => x.RegistrationDate).DisplayFormat("{0:yy-MMM-dd}");

            Column(x => x.MarketShare);

            Column(x => x.NumberOfEmployees).DisplayFormat("{0:n0}");

            Column(x => x.Country);

            ButtonColumn("Edit").Icon(FA.Edit)
                .OnClick(x => x.Go<Company.EnterPage>()
                .Send("item", "item.ID")
                .SendReturnUrl());

            Button("New Company").Icon(FA.Plus)
                .OnClick(x => x.Go<Company.EnterPage>().SendReturnUrl());
        }
    }
}
```

Like above, we use `DisplayExpression()` method to show the date format how we want.

### Country Page

Add a *root page* named **Country** under **Pages** folder of **#UI** using M# context menu (or any oher way that you are comfortable with):

```C#
using MSharp;
public class CountryPage : RootPage
{
    public CountryPage()
    {
        Add<Modules.CountriesList>();
    }
}
```

Now add a folder named **Country** under **Pages** folder, then add an **Enter** *sub page* class:

```C#
using MSharp;

namespace Country
{
    public class EnterPage : SubPage<CountryPage>
    {
        public EnterPage()
        {
            Add<Modules.CountryForm>();
        }
    }
}
```

#### Creating required module of Country Page

Move on to **Modules** folder of **#UI** and add a folder with the name of **Country** which will contain related modules of *country* view.
Now use M# context menu and add a *form module* named **CountryForm**:

```C#
using MSharp;

namespace Modules
{
    public class CountryForm : FormModule<Domain.Country>
    {
        public CountryForm()
        {
            HeaderText("Country details");

            Field(x => x.Name);

            Field(x => x.Code);

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

And also a *listmodule* named **CountriesList**:

```
using MSharp;

namespace Modules
{
    public class CountriesList : ListModule<Domain.Country>
    {
        public CountriesList()
        {
            HeaderText("Countries");

            Column(x => x.Name);

            Column(x => x.Code);

            ButtonColumn("Edit").Icon(FA.Edit)
                .OnClick(x => x.Go<Country.EnterPage>()
                .Send("item", "item.ID")
                .SendReturnUrl());

            Button("New Country").Icon(FA.Plus)
                .OnClick(x => x.Go<Country.EnterPage>().SendReturnUrl());
        }
    }
}
```

Now we are done with views.

#### Adding Pages to Menu

After you ended up with form page, you need to add it to the main menu:

```C#
using MSharp;

namespace Modules
{
    public class MainMenu : MenuModule
    {
        public MainMenu()
        {
            AjaxRedirect().IsViewComponent().UlCssClass("nav navbar-nav dropped-submenu");

            Item("Login")
                .Icon(FA.UnlockAlt)
                .VisibleIf(AppRole.Anonymous)
                .OnClick(x => x.Go<LoginPage>());

            Item("Settings")
                .VisibleIf(AppRole.Admin)
                .Icon(FA.Cog)
                .OnClick(x => x.Go<Admin.SettingsPage>());

            Item("Register")
                .Icon(FA.Cog)
                .OnClick(x => x.Go<RegistrationPage>());

            Item("Companies")
                .Icon(FA.Cog)
                .OnClick(x => x.Go<CompanyPage>());

            Item("Countries")
                .Icon(FA.Cog)
                .OnClick(x => x.Go<CountryPage>());
        }
    }
}
```

### Final Step

Build **#UI** project, set the **WebSite** project as your default *StartUp* project and configure your *connection string* in **appsetting.json** file and hit F5. Your project is ready to use.



