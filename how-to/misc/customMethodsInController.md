# Custom Methods In Controller

## Problem

You want to handle logic for a page, using a method that is only available within the page's controller.

For example, an Accounts user has a list of Invoices to indicate whether or not they have already been paid. The user selects invoices that are not yet paid and then clicks the "Mark as Paid" button, which updates the invoices via a method in the controller and reloads the list.

## Implementation

This is possible via `OnControllerClassCode()`, which will create new code that gets generated for the controller.

Using the above example, a custom method can be created as follows:

```csharp
OnControllerClassCode("Pay selected invoices")
    .Code(@"public async Task PayInvoices(vm.InvoicesList info)
    {
        var selected = await info.SelectedItems;

        /*
        * Rest of code
        */
    }");
```

The parameter used for `OnControllerClassCode()` defines the comment that will go along with your code.

The `Code()` method is used alongside `OnControllerClassCode()` and handles the code that you want to add to your controller.

The above will generate the following in your controller:

```csharp
// Pay selected invoices
public async Task PayInvoices(vm.InvoicesList info)
{
    var selected = await info.SelectedItems;

    /*
    * Rest of code
    */
}
```

> **Note:** When using the `Code()` method, because MSharp generates the code for the controller regardless of what you provided for the method in the UI project, any errors in the code would only get picked up in the Website project.

The new custom method can then be called within the module:

```csharp
Button("Mark as Paid")
    .OnClick(x =>
    {
        x.CSharp("await PayInvoices(info);").ValidationError();
        x.GentleMessage("Selected invoices paid.");
        x.Reload();
    });
```
