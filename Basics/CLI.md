# M# Command Line Interface

**M# CLI** is a command line interface to scaffold and build M# apps. Not only it provides you scalable project structure, instead it handles all common tedious tasks for you out of the box.

## Getting Started

M# CLI ships with handful of commands to set up and build your project from scratch, after creating your project go to this path: **M#\lib\netcoreapp2.0**. This folder is located in your project root path, run below command to see if you have done everything good.

!["M# CLI"](CliImage/MSharpCLI.PNG "M# CLI")

By running **msharp.exe** you will see all options and outputs and how to use them.

### msharp.exe /build *[/model]* *[/ul]*

By running **msharp.exe /build** m# framwrok will try to compile your current project and show you the result. If your project encounters any errors, you will see the result here.
For example, in following picture you can see that current project has an error an you will see the detail:

!["M# CLI Error Detail"](CliImage/CLIErrorDetail.PNG "M# CLI Error Detail")

If you want to build just *#Model* or *#UI* project you can use this command:

- msharp.exe /build /model
- msharp.exe /build /ui

### msharp.exe /add:type /name:"TypeName" [/base:"BaseTypeName"] [/folder:"ContainerFolder"]

This command lets you generate entity in *#Model* project. For example, we have generated *Motor* entity with the following command:

- msharp.exe /add:type /name:"Motor"

If you want your generated entity placed in a specific folder or inherit from other entity, use these optional parameters:

- /base: use this for inheritance.
- /folder: use this for generating output in specific folder.

For example, in this sample we have generated *Motor.cs* class that inherits from *Vehicle* and generate output in *Domain* folder:

- msharp.exe /add:type /name:"Motor" /base:"Vehicle" /folder:"Model/Domain"

### msharp.exe /add:form /on:"EntityTypeName" /name:"MyFormName" [/folder:"ContainerFolder"]

This command creates **form module** in *#UI* project base on selected entity. For example, in the following command we are going to create *MotorForm* module:

- msharp.exe /add:form /on:"Motor" /name:"MotorForm"

The generated output file is shown bellow:
!["M# CLI Form"](CliImage/FormCli.PNG "M# CLI Form")

### msharp.exe /add:view /on:"EntityTypeName" /name:"MyFormName" [/folder:"ContainerFolder"]

This command creates **view module** in *#UI* project base on selected entity. For example, in the following command we are going to create *MotorView* module:

- msharp.exe /add:view /on:"Motor" /name:"MotorView"

The generated output file is shown bellow:
!["M# CLI View"](CliImage/ViewCli.PNG "M# CLI View")

### msharp.exe /add:list /on:"EntityTypeName" /name:"MyFormName" [/folder:"ContainerFolder"]

This command creates **list module** in *#UI* project base on selected entity. For example, in the following command we are going to create *MotorList* module:

- msharp.exe /add:list /on:"Motor" /name:"MotorList"

The generated output file is shown bellow:
!["M# CLI List"](CliImage/ListCli.PNG "M# CLI List")

### msharp.exe /add:menu /name:"MyLMenuName" [/folder:"ContainerFolder"]

This command creates **menu** in *#UI* project. For example, in the following command we are going to create *MotorMenu*:

- msharp.exe /add:menu /name:"MotorMenu"

The generated output file is shown bellow:
!["M# CLI Menu"](CliImage/MenuCli.PNG "M# CLI Menu")

### msharp.exe /add:page /name:"PageName" [/parent:"FullPathToParentFolderOrFile"]

This command creates **page** in *#UI* project. For example, in the following command we are going to create *MotorPage*:

- msharp.exe /add:page /name:"MotorPage"

The generated output file is shown bellow:
!["M# CLI Page"](CliImage/PageCli.PNG "M# CLI Page")