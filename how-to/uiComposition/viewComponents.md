# View Components

## Problem

You have a module shown on multiple pages. For example, you have a Patient View module that should be visible at the top of multiple pages specific to individual Patients.

## Implementation

There are 2 different ways to do this

1) Simply Add the Module to multiple Pages.

```csharp
    Add<Modules.PatientView>();
    Add<Modules.PatientProceduresList>();
```

When you add a module to multiple pages MSharp removes the module’s code from the Page controller and makes a separate Module Controller. This allows the same module to be added to multiple pages without repeating code.

2) Make the module a View Component. You do not always want to Add() the module to individual pages.

```csharp
        public Footer()
        {
            IsViewComponent();

            /*
             * other code
             */
        }
```

Now MSharp will generate all the necessary controllers and bindings without it needing to be explicitly added to a page in the UI. ViewComponent controllers are generated in Website > Views > Modules > Components.

Now it can instead be invoked from a Layout page or from inside Markup.

```csharp
    <footer>@await Component.InvokeAsync(typeof(Footer))</footer>
```
View Components are particularly suited to
-	Dynamic menus
-	Login panels
-	Shopping carts 
