# MSharp Docs

> Note 1: Read [CONTRIBUTING.md](CONTRIBUTING.md) if you want to participate in M# documentation.

> Note 2: M# is based on the [Olive Framework](https://geeksltd.github.io/Olive/#/) which you must learn in order to use M#.

## Tutorials

### [Intro - What is M#](Overview/README.md)

### [Intro - Installation](Install/README.md)

### [M# Tutorial - Episode 1: Your First App](Tutorials/1/README.md)

In this lesson you will learn about the key M# concepts:

- Entity type creation (including associations)
- Page & menus and navigation
- List modules, form modules and buttons

### [M# Tutorial - Episode 2: Modal pages](Tutorials/2/README.md)

In this lesson you will learn about:

- Menu
- Pop-up (modal) pages
- Image and file properties

### [M# Tutorial - Episode 3: Uniqueness rules](Tutorials/3/README.md)

In this lesson you will learn about:

- Uniqueness rules

### [M# Tutorial - Episode 4: Search](Tutorials/4/README.md)

In this lesson you will learn about:

- Property search element
- All fields search element
- Custom Label for form / search elements

### [M# Tutorial - Episode 5: Inheritance](Tutorials/5/README.md)

In this lesson you will learn about:

- Inheritance
- Export to excel
- Client-side filter
- Index column

### [M# Tutorial - Episode 6: Advanced Associations](Tutorials/6/README.md)

In this lesson you will learn about:

- One to Many (inverse) associations
- Many to Many associations

### [M# Tutorial - Episode 7: Validation and pagination](Tutorials/7/README.md)

In this lesson you will learn about:

- Range validation
- Paging
- Button style (link)
- Property setter
- Expected lines

### [M# Tutorial - Episode 8: Calculated properties](Tutorials/8/README.md)

In this lesson you will learn about:

- Footer
- Cascade delete
- Calculated property

### [M# Tutorial - Episode 9: Master-detail](Tutorials/9/README.md)

In this lesson you will learn about:

- Master-detail forms

### [M# Tutorial - Episode 10: List data source](Tutorials/10/README.md)

In this lesson you will learn about:

- List data source
- View module property
- Link button

### [M# Tutorial - Episode 11: Method logic](Tutorials/11/README.md)

In this lesson you will learn about:

- Html.Raw
- Empty markup
- Method logic

### [M# Tutorial - Episode 12: Advanced validation](Tutorials/12/README.md)

In this lesson you will learn about:

- Validate() method of objects
- Form level custom validation
- Form element header markup
- Module header text

### [M# Tutorial - Episode 13: Form element](Tutorials/13/README.md)

In this lesson you will learn about:

- Control type
- Form element data source
- Form element source criteria

### [M# Tutorial - Episode 14: Sending email](Tutorials/14/README.md)

In this lesson you will learn about:

- Boolean form element (true, false text)
- Custom workflow action
- Sending emails
- Email Templates

### [M# Tutorial - Episode 15: Formatting property](Tutorials/15/README.md)

In this lesson you will learn about:

- List column format (date and percentage, and number separator)
- Form element display expression
- Search element display expression

### [M# Tutorial - Episode 16: Form wizard](Tutorials/16/README.md)

In this lesson you will learn about:

- Mandatory property, but optional on a form
- Optional property, but mandatory on a form
- Setting a form value automatically only if the user didn't.
- Interactive image (using buttons)
- Custom search behavior

### [M# Tutorial - Episode 17: Dynamic menu](Tutorials/17/README.md)

In this lesson you will learn about:

- Dynamic menu item
- Custom Active menu item
- Visibility
- Module box
- After control, Before control settings

### [M# Tutorial - Episode 18: Automated tasks](Tutorials/18/README.md)

In this lesson you will learn about:

- Repeated buttons
- Button markup template
- Checkbox column for list modules
- Display option for columns
- Instance accessor for entity types
- Automated tasks

## Structure Tutorial

### Business Domain - Basics

- [Understanding Entity Types](Domain/UnderstandingEntityTypes.md)
- [Properties](Domain/Properties.md)
- [Inheritance](Domain/Inheritance.md)
- [Transient, Interface, Abstract](Domain/Transient.md)
- [Generated Code](Domain/GeneratedCode.md)
- [Partial Class & Business Logic](Domain/PartialClass.md)
- [String Property](Domain/StringProperty.md)
- [DateTime Property](Domain/DateTimeProperty.md)
- [Associations](Domain/Associations.md)
- [Number Property](Domain/NumberProperty.md)
- [File](Domain/File.md)
- [Boolean](Domain/Boolean.md)
- [Calculated Properties](Domain/CalculatedProperties.md)

### Business Domain - Advanced

- [The role of ID](Domain/Advanced/TheRoleOfId.md)
- [The role of IsNew](Domain/Advanced/TheRoleOfIsNew.md)
- [The role of ToStringExpression()](Domain/Advanced/TheRoleOfToString.md)
- [IEntity interface](Domain/Advanced/IEntityInterface.md)
- [TransientEntity](Domain/Advanced/TransientEntity.md)
- [MSharp Interfaces](Domain/Advanced/MSharpInterface.md)

### Working with Data

- [Database.Get() VS Database.Find()](Data/DatabaseGet.md)
- [Database.GetList()](Data/DatabaseGetList.md)
- [Database.Save()](Data/DatabaseSave.md)
- [Database.Update()](Data/DatabaseUpdate.md)
- [Database.Delete()](Data/DatabaseDelete.md)
- [Database.Any(), None() and Count()](Data/DatabaseAnyNoneCount.md)
- [ConnectionString and config](Data/ConnectionString.md)
- [Working with existing databases](Data/WorkingWithExistingDatabase.md)

### UI Structure 

- [Master Page](UI/MasterPage.md)
- [Modal VS Standard](UI/ModalVSStandard.md)
- [Module Hosting](UI/ModuleHosting.md)
- [OnStart()](UI/OnStart.md)
- [Page Settings](UI/PageSettings.md)

### We will have more and more titles

Soon™ ...

## Useful Tips

### [M# CLI (msharp.exe)](Basics/CLI.md)

Learn how to use the msharp.exe CLI (Command Line Interface) to diagnose problems, or automate things.

### [Shortkeys & Editing tips](Basics/Tips.md)

Learn tips and tricks to speed you up and make your life easier when developing M# apps in Visual Studio.

### [Merging action list buttons](how-to/MergeColumns.md)

By default, **M#** generate each action button to a seperate table cell. but, if you have lots of action buttons you may prefer to merge them in one cell...

### [Using global search](how-to/UsingGlobalSearch.md)

This feature let you globally search through your application and navigate to your destination page.
