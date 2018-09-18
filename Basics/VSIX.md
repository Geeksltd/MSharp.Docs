# M# Visual Studio Extensions
(todo: intro)

(todo: for each single feature in this extension, add a section here with screenshots, etc. Also provide a CLI alternative tip for doing the same thing in CMD)

## VS Ext: MSharp.AddNew
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

![alt text](images/NewMSharpClassLibraryTemplate.png)

# Generate Project Items
Depending on the type of project chosen, developers can create/add custom project requirements by using M# context menu of a solution explorer node.

## Create New Entity
In each M# project the first thing a developer needs to do is to build a concrete business domain model, which consists of entities often referred to as business objects, in this case developer can select a node (Project root node/Folder) from solution explorer tree in the __#Model__ project then right click on it and choose **"Add Entity ..."** from path "Add > M# > Add Entity ..." menu item of it's context menu.

![alt text](images/AddNewEntity.PNG)


M# shows a tool window to get an _Entity/**Type Name**_ with an optional __Base Type__ to generate a plain __M# Entity__ class or a generic __M# Entity SubType__ class under selected node.

![alt text](images/CreateNewEntityWindow.png)

So that if developer only specified a __Type Name__ then M# creates a plain Enity type class and if he select a __Base Type__ from dropdown combo then M# will generates a Entity __SubType<*Base Type*>__ class depending on selected item.

> Note : Only compiled Entity Types are availabe in drop down combo to select as Base Type.

## VS Ext: MSharp.Colorize
By using __MSharp.Colorize__ extension all M# Projects (MVC, MVC Microservice and Class Library) has specific UI layout in solution explorer tool window. So that Model and UI projects in "M# ASP.NET - MVC" and "M# ASP.NET - MVC Microservice" and project root icon in "M# Class Library" are shown as a simple custom M# purple icon like this : 

![alt text](images/MSharpMVCSolutionExplorer.PNG)


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

## Vs Ext: Geeks.StylishCode
...

## M# Project Templates
...
