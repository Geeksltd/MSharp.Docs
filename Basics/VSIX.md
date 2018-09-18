## M# Visual Studio Extensions
(todo: intro)

(todo: for each single feature in this extension, add a section here with screenshots, etc. Also provide a CLI alternative tip for doing the same thing in CMD)

# VS Ext: MSharp.AddNew
MSharp.AddNew VSIX provides a set of functionality and project templates wizards to make projects from scratch and create M# project items easily. So you can create 3 different M# project types (**M# ASP.NET Core - MVC**, **M# ASP.NET Core - Microservice** and **M# Class Library**) by using this extension.

![alt text](images/NewProjectTemplates.png "New Project Tempates")

## ![](images/MSharp.png) ASP.NET Core - MVC Project
---
By using **_M# MVC Project Template Wizard_** you can create a standard M# project from scratch. Each M# ASP.NET MVC Application at least should consists of 4 different projects. 

* #Model *(Standard .Net Core 2.1)*
* #UI *(Standard .Net Core 2.1)*
* Domain *(Standard .Net Core 2.1)*
* Website *(Standard ASP.Net Core App 2.1)*
* _[Docker-compose]_ *(Docker Contianer)*

Developers should specify the _Name_, _Location_ and _Solution name_ of new project and hit **OK** button, then a project wizard with a popup winodow gets custom __M#__ project options from user In the **M# MVC Project Wizard** window.

![alt text](images/NewMSharpMVCProjectWizard.png "M# MVC Project Wizard")

In **M# MVC Project Wizard** window developers should specify a **M# Project Name** and choose a **Database Type** providers such as _Sql Server_, _MySQL_, _PostgreSQL_, _Sqlite_ as Database Management System for new M# Application. Also developers should specify related **Connections String** according to selected **Database Type** as well.

![alt text](images/NewMSharpMVCProjectWizard_DB.png "M# MVC Project Wizard DB Select")

Then M# project wizard tries to download new fresh copy of __M# MVC Project__ template from web server.

![alt text](images/DownloadProgressWindow.png "Downloading Window")

After the template downloaded successfully, **Initialize.bat** of downloaded package automatically runs to initialize M# solution by updating projects referenses and all required website packages.

![alt text](images/SolutionInitialization.png "Downloading Window")

## ![](images/MSharp.png) ASP.NET Core - MVC Microservice Project
---
By using **_M# ASP.NET Core MVC Microservice Project_** you can create a standard M# Microservice project from scratch. Each M# ASP.NET Microservice Application at least should consists of 4 different projects. 

* #Model *(Standard .Net Core 2.1)*
* #UI *(Standard .Net Core 2.1)*
* Domain *(Standard .Net Core 2.1)*
* Website *(Standard ASP.Net Core App 2.1)*

Developers should specify the _Name_, _Location_ and _Solution name_ of new project and hit **OK** button, then a project wizard with a popup winodow gets custom __M# Microservice__ project options from user In the **M# Microservice Project Wizard** window.

![alt text](images/NewMSharpMiscroserviceProjectWizard.png "M# Microservice Project Wizard")

In **M# Microservice Project Wizard** window developers should specify a **M# Microservice Project Name** and choose a **Database Type** providers such as _Sql Server_, _MySQL_, _PostgreSQL_, _Sqlite_ as Database Management System for new M# Microservice Application. Also developers should specify related **Connections String** according to selected **Database Type** as well.

![alt text](images/NewMSharpMicroserviceProjectWizard_DB.png "M# MVC Project Wizard DB Select")

Then M# project wizard tries to download new fresh copy of __M# MVC Microservice Project__ template from web server.

![alt text](images/DownloadProgressWindow.png "Downloading Window")

## ![](images/MSharp.png) Class Library Template
---
We have produced a __Custom Project Sub Type__ with name "M# Class Library Template", developers can use this project type as a standard class library in their .NET framework projects.

![](images/NewMSharpClassLibraryTemplate.png)

# Build All

![](images/BuildAllMenuItem.PNG)


# Generate Project Items
Depending on the type of project chosen, developers can create/add custom project requirements by using M# context menu under solution explorer node.

## Create New Entity
In each M# project the first thing a developer needs to do is to build a concrete business domain model, which consists of entities often referred to as business objects, in this case developer can select a node (Project root node/Folder) from solution explorer tree in the __#Model__ project then right click on it and choose **"Add Entity ..."** from path "Add > M# > Add Entity ..." menu item of it's context menu.

![](images/AddNewEntity.PNG)


M# shows a tool window to get an _Entity/**Type Name**_ with an optional __Base Type__ to generate a plain __M# Entity__ class or a generic __M# Entity SubType__ class under selected node.

![](images/CreateNewEntityWindow.png)

So that if developer only specified a __Type Name__ then M# creates a plain Enity type class and if he select a __Base Type__ from dropdown combo then M# will generates a Entity __SubType<*Base Type*>__ class depending on selected item.

> Note : Only compiled Entity Types are availabe in drop down combos to select as Base Type in all Create pages.

> [![](images/CLI.png "M# Command Line Interface") CLI Command](CLI.md#user-content-msharpexe-addtype-nametypename-basebasetypename-foldercontainerfolder) : 
>
> msharp.exe /add:type /name:"Person" [/base:"Administrator"] [/folder:"ContainerFolder"]
>- _Person is sample entity name_
>- _Administrator is sample entity base type_ (optional)
>- _ContainerFolder is sample folder_ (optional)

## Create CRUD

![](images/CreateCRUD.PNG)
![](images/CreateCRUDWindow.PNG)

> [![](images/CLI.png "M# Command Line Interface") CLI Command](CLI.md) : 
>
> msharp.exe /add:Crud /page:"Admin.cs" /type:"ContentBlock" [/menu:"MainMenu"]
>- _Admin.cs is sample page name_
>- _ContentBlock is sample entity base type_
>- _MainMenu is sample menu module name_ (optional)

## Create Partial Class

![](images/CreatePartialClass.PNG)

## Create Form 
![](images/AddFormMenu.PNG)
![](images/AddFormWindow.PNG)

> [![](images/CLI.png "M# Command Line Interface") CLI Command](CLI.md#user-content-msharpexe-addform-onentitytypename-namemyformname-foldercontainerfolder) : 
>
> msharp.exe /add:form /on:"EntityTypeName" /name:"MyFormName" [/folder:"ContainerFolder"]
>- _EntityTypeName is sample entity name_
>- _MyFormName is sample form module name_
>- _ContainerFolder is sample folder_ (optional)
## Create List 
![](images/AddListMenu.PNG)
![](images/AddListWindow.PNG)

> [![](images/CLI.png "M# Command Line Interface") CLI Command](CLI.md#user-content-msharpexe-addlist-onentitytypename-namemyformname-foldercontainerfolder) : 
>
> msharp.exe /add:list /on:"EntityTypeName" /name:"MyListName" [/folder:"ContainerFolder"]
>- _EntityTypeName is sample entity name_
>- _MyListName is sample list  module name_
>- _ContainerFolder is sample folder_ (optional)

## Create View 
![](images/AddViewMenu.PNG)
![](images/AddViewWindow.PNG)

> [![](images/CLI.png "M# Command Line Interface") CLI Command](CLI.md#user-content-msharpexe-addview-onentitytypename-namemyformname-foldercontainerfolder) : 
>
> msharp.exe /add:view /on:"EntityTypeName" /name:"MyViewName" [/folder:"ContainerFolder"]
>- _EntityTypeName is sample entity name_
>- _MyViewName is sample view module name_
>- _ContainerFolder is sample folder_ (optional)

## Create Menu 
![](images/AddMenuMenu.PNG)
![](images/AddMenuWindow.PNG)

> [![](images/CLI.png "M# Command Line Interface") CLI Command](CLI.md) : 
>
> msharp.exe /add:menu /name:"MyMenuName" [/folder:"ContainerFolder"]
>- _MyMenuName is sample menu module name_
>- _ContainerFolder is sample folder_ (optional)

## Create Generic Module
![](images/AddGenericModuleMenu.PNG)
![](images/AddGenericModuleWindow.PNG)

> [![](images/CLI.png "M# Command Line Interface") CLI Command](CLI.md) : 
>
> /add:Custom /name:MyCustomModule /folder:"C:\..\MSharp.Mvc\M#\UI\Modules"
>- _MyCustomModule is sample generic module name_
>- _C:\..\MSharp.Mvc\M#\UI\Modules is sample folder path that module should create there_ (optional)

## Create Root Page
![](images/AddPageMenu.PNG)
![](images/AddPageWindow.PNG)

> [![](images/CLI.png "M# Command Line Interface") CLI Command](CLI.md) : 
>
> msharp.exe /add:page /name:"PageName" [/parent:"FullPathToParentFolderOrFile"]
>- _PageName is sample page or sub-page module name_
>- _FullPathToParentFolderOrFile is sample folder or Page Module file name_

## Create Sub-Page
![](images/AddSubPageMenu.PNG)
![](images/AddSubPageWindow.PNG)

> [![](images/CLI.png "M# Command Line Interface") CLI Command](CLI.md) : 
>
> msharp.exe /add:Page /name:MySubAdmin /parent:"C:\...\MSharp.Mvc73\MSharp.Mvc\M#\UI\Pages\Admin.cs"
>- _MySubAdmin is sample Sub Page name_
>- _C:\..\MSharp.Mvc73\MSharp.Mvc\M#\UI\Pages\Admin.cs is sample Parent Page full path_

## Create CRUD by Page
![](images/PageCreateCRUDMenu.PNG)
![](images/PageCreateCRUDWindow.PNG)


> [![](images/CLI.png "M# Command Line Interface") CLI Command](CLI.md) : 
>
> msharp.exe /add:Crud /page:"Admin.cs" /type:"Administrator" [/menu:"AdminSettingsMenu"]
>- _Admin.cs is sample page name_
>- _Administrator is sample entity base type_
>- _AdminSettingsMenu is sample menu module name_ (optional)

## Create API Proxy
![](images/GenerateApiProxyMenu.PNG)
![](images/GenerateApiProxyWindow.PNG)

> [![](images/CLI.png "M# Command Line Interface") CLI Command](CLI.md) : 
>
> msharp.exe /add:type /name:"Person" [/base:"Administrator"] [/folder:"ContainerFolder"]
>- _Person is sample entity name_
>- _Administrator is sample entity base type_
>- _ContainerFolder is sample folder_

# VS Ext: MSharp.Colorize
![](images/MSharp.png) By using __MSharp.Colorize__ extension all M# Projects (MVC, MVC Microservice and Class Library) has specific UI layout in solution explorer tool window. So that Model and UI projects in "M# ASP.NET - MVC" and "M# ASP.NET - MVC Microservice" and project root icon in "M# Class Library" are shown as a simple custom M# purple icon like this : 
 
![](images/MSharpMVCSolutionExplorer.PNG)

Also according to C# class file contents and it's base class in #Model and #UI projects, their icon will be changed in this types:
- ![](images/CsType.png) : Plain __C#__ files
- ![](images/EntityType.png) : M# __Entity__ Type and Entity __SubType<*base*>__ 
- ![](images/FormModule.png) : M# __Form Module__
- ![](images/ListModule.png) : M# __List Module__
- ![](images/MenuModule.png) : M# __Menu Type__ and __Menu Module__
- ![](images/ViewModule.png) : M# __View Module__
- ![](images/RootPage.png) : M# __Root Page__ and __SubPage__
- ![](images/GenericModule.png) : M# __Generic Module__
  
  >These icons are shown in Top Right corner of each M# class modules in code editor window too, for example in M# Entity file it will be look like this : 

  ![](images/EntityTextEditorSample.PNG)



## Vs Ext: Geeks.StylishCode
...

## VS Ext: MSharp.CodePreview 
...


## VS Ext: MSharp.F7 
...

## VS Ext: MSharp.Goto 
...

## VS Ext: MSharp.Intellisense 
...

## VS Ext: MSharp.Snippet 
...

## VS Ext: MSharp.Warninigs 
...

## VS Ext: MSharp.CodePreview 
...


## M# Project Templates
...
