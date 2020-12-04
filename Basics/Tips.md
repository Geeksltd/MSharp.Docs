# M# Shortkeys and Editing Tips

A set of tips to make your more productive.

## Intellisense for custom code fragments

In M# in many places you can add C# code in the middle of your M# definitions. For example to specify the default value for a property.

Let's say you have the following definition:

```csharp
public class SomeType: EntityType
{
        public SomeType()
        {
            ...
            DateTime("Date").Mandatory().Default("C#:LocalTime.Now");
        }
}
```

In the above example, the default value expression is a **constant string**, which ultimately will be generated in the target Domain entity code. So you know that its true *nature* is a ***C# expression***, while in the M# definition file, it's just plain string. It would be often handy to use intellisense for code completion and checking write at this level to ensure your code fragment is valid.

1. Put the cursor anywhere on the text, i.e. "C#:LocalTime.Now".
2. Press Alt + i
3. A small pop-up window will appear, giving the context of the target code, enabling full intellisense.
4. Write the code and press Ctrl + S.
5. The pop-up will automatically hide.
6. In the above example, the new code will appear as the argument of Default() method.

## Jump to related files using F7

Thanks to the [M# F7](https://marketplace.visualstudio.com/items?itemName=Paymon.SmartF7) visual studio extension, you can quickly jump between sister files in a group of related files in Visual Studio.

For example if you're editing an M# Entity type, pressing F7 (multiple times) will rotate between the following sister files:

- @Model{namespace}\Customer.cs
- Domain\Entities\Customer.cs
- Domain-Logic\Customer.cs

It works with pages, modules and entities.

## Where is {Property} used

If you press ***Ctrl + .*** with your cursor on an M# property definition line, you will see some Quick Action snippets appearing on the left hand side reading **"Where is *{PropertyName}* used?"**.
When you click it, it will jump onto the generated code for that property (in the *Domain\[Gen-Entities]* folder) and then finds all references to that.

This way you can see where that property is used in:

- Business logic
- M# UI objects (Forms, Lists, Views)

> This works in the other way around also. You can jump from a generated property's code into its M# definition by pressing **Ctrl + .**

## Faster running and debugging

When you use F5 in Visual Studio to run the project, it will always build the website again which is a slow process. If you have manually compiled the projects using Shift + F6 already and you just want to run the website, you can:

- In Solution Explorer right click on the Website
- Select Just Run

## Metadata hook
When you define your #M#\Model and M#\UI projects, your M# definitions are typically defined as C# types. Those are serialized into XML when you run `dotnet msharp.dsl.dll` with either `/model` or `/ui` options. The generated XML is then used by `msharp.exe` to get the M# metadata objects and generate the application code.

It is possible to hook into this process. Just before the XML is generated, an event will be fired called `MSharp.Repo.BeforeSerialize`. You can handle this event by writing your code in the static constructor of any of your M# definitions. Example:

```csharp
class HomePage : RootPage
{
   ... 
   static HomePage()
   {
       MSharp.Repo.BeforeSerialize += Hook;
   }
   
   static void Hook()
   {
       foreach(var page in MSharp.Repo.Everything.OfType<MSharp.ApplicationPage>())
          page.Roles(AppRole.TaDa);
   }
}
```
