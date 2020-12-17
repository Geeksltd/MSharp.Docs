# Migrating from Json (web-based IDE) to MC# (Visual Studio based)

To convert an existing application to the new model, you need to convert the meta-data into the new format (*MC# files*) and then delete the old meta-data files (*.msharp files*).

### Step 1: Prepare
1. Open the project in the old M# as before and build everything.
2. Open the solution in Visual Studio.
	- For all projects in the solution, go to properties window and change it to `.NET 4.7.2`
	- Update `MSharp.Framework` nuget packages to the latest version
	- In Website, add the nuget package: `Microsoft.CodeDom.Providers.DotNetCompilerPlatform` if it has not been referenced before
	- Open `web.config` and change connection string to use `MyProject.Temp` as the DB name, and `.\SqlExpress`
	- Compile everything.
		- In this step, if you get an error related to the enum values, you can simply comment those parts and after adding *#Model* project you can specify enum values in the `InstanceAccessors(..)` method and then uncomment those parts again.

### Step 2: Model -> Domain (WebForms only)
If your project is WebForms, perhaps your domain model project name is **"Model"** instead of **"Domain"**. You should change it to **"Domain"**:

1. In the project settings in M# IDE, set _Model Project Folder_ to **"Domain"**
2. _Visual Studio:_ Remove the Model project from the solution and save everything.
3. Rename the folder from Model to Domain
4. Rename the csproj file inside that folder to also Domain
5. In Visual Studio, right click on the solution and choose _Add > Existing project_ and select the new `Domain.csproj` file.

### Step 3: Convert Meta-data

1. Close the project in IDE 
2. Copy MSharpTools to your computer.
3. Run msharptools.exe "{solutionRoot}" /mcs
	- It will create a new folder in the solution named **M#**. Inside that, it will generate two new folders: **Model** and **UI**.
3. In Visual Studio, use **Add Existing** project and add `M#\Model` and `M#\UI` projects to the solution.
	- If `#Model > ProjectSettings.cs` has `.GeneratedDALFolder("DAL")` method, please comment it.
4. In Visual Studio, go to Manage Nuget packages and click on the Restore button at the top.
	- Sometimes even after restoring nuget packages some of them are not loaded completely, if you experience this issue you should use `Update-Package -reinstall` command in the *Package Manager Console*.
5. In the Domain project, include the newly generated **[DEV-SCRIPTS]\ReferenceData.cs**
6. In `TheApplication.cs` (or `Global.asax` in Web Forms) add the following:

```csharp
protected override void InitiateApplication()
{
     MSharp.Framework.Services.TestDatabaseGenerator.CreateReferenceData = ReferenceData.Create;
     base.InitiateApplication();
}
```

### Step 4: Clean up
1. Remove the **Entities** folder from the **Domain** project.
2. Remove the **Mappings** or **DAL** folder from the **Domain** project.
3. Delete the old folder **@M#** as it's no longer used in the new model.
	- _NOTE: If you have changed anything in the Manual folder, you should manually move that to the new model._
4. In the **gitignore** file, add M#/lib/
	- Also ensure that all obj and bin folders are excluded.
5. Update app setting in web.config file of website project:

```xml
<add key="M#.Meta.Location" value="C:\Projects\[YOURProjectNAME]\DB" />
```

Depending on your project you may need to add this part too:

```xml
<add key="Temp.Databases.Location" value="C:\@Database.Files" />
```

### Step 5: Verify the result
In Visual Studio, compile the following projects in the following order:

 1. #Model
 2. Domain
 3. #UI
 4. Website

If you faced any problem, please report to Paymon immediately. Otherwise you're good to go.

### Troubleshooting

- Learn to use the [M# CLI](http://learn.msharp.co.uk/#/Basics/CLI) to diagnose problems
- If your application has an entity named "Project", rename the generated #Model\Project.cs class to "OverallProject".

Also consider the following architectural changes:

| Old M# | The MC# way |
|:-:|:-:|
| **@M#\*.msharp**: These json files defined your M# elements such as entity types, pages, modules, etc | The metadata is defined as C# files inside the #Model and #UI projects |
| **@M#\Tables\*.Create.sql**: These files defined your application database schema. When you loaded a project in the M# Agent app, it read the above files and create a database named MyApp.DesignTime from the schema | Entity definitions are enough. Upon building the #Model project, M# will generate the schema of the database into \DB folder. |
| **@M#\Tables\*.Data.sql**: These SQL files contained your reference data. Upon loading a project, these were inserted into the MyApp.DesignTime database. | Reference data is defined as C# code rather than SQL files inside ReferenceData.cs class. |


# Migrating apps from .NET Framework to .NET Core

1. First convert the application to MC#
1. Create a new M# .NET Core app
1. Copy these files from the converted MC# app to the newly generated .NET Core app:
   - M#\Model\*.*
   - M#\UI\*.*

## Renamed namespaces, types & methods
The following elements are renamed in the framework. In your application, you should change all references to the old names.
- MSharp.Framework → Olive
- Database.Find() → Database.FirstOrDefualt()
- Document → Blob
- IEmailQueueItem → IEmailMessage 
- IApplicationEvent → IAuditEvent 
- IHttpActionResult → IActionResult or Task<IActionResult>
- RoutePrefix(Attribute) → Route(Attribute).
- [Authorized] → [JwtAuthenticate]

## Tips:
- Most extension methods which were defined in the System (namespace) before. Now they are in Olive. When you face missing methods, check the suggested using-list.
- Many methods are changed to async. When your method calls them, your method should also become async. This is recursive all the way up.
- If you use email sending:
  - If your new app is a monolithm add a NuGet reference to `Olive.Email` package
  - If your new app is a Microservice, just reference the `EmailService.EmailApi` nuget package and use that, similar to other microservices.
	- Replace all `Database.Save(new EmailQueueITem....` with `EmailApi.Fresh().Send(new Email {` 
- If your new app is a Microservice, remove `ApplicationEvent` entity. Logging is handled centrally in Microservices (in Audit service).
- Instead of using User in the controllers and views to reference the current user use GetUser() method.
