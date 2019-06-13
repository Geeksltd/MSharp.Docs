# Transactions

## Problem

There will be instances in an application where you will want certain actions to be performed only if other actions occur.

A way to do this is to put these actions into a transaction, meaning that the transaction will only be performed if all actions are successful.

## Implementation

In M# we have the `CreateTransactionScope()` method we can use to encapsulate areas of our code.

### Example

Below is the structure you can apply to use this method.

```csharp
using (var scope = Database.CreateTransactionScope())
    {
        //Add code here

        scope.Complete();
    }
```

We can add anything we wish to occur together.

```csharp
 using (var scope = Database.CreateTransactionScope())
    {
        if ((User.IsInRole("Adviser") || User.IsInRole("Admin") || !CurrentApplication.IsSubmitted()))
            {
                    try
                    {
                        if (!await SaveInDatabase(info)) return JsonActions(info);
                    }
                        catch (Olive.Entities.ValidationException ex)
                    {
                        return Notify(ex.Message, "error");
                    }
                    try
                    {
                        await new MortgageApplicationService(info.Item.Application).MarkAsFurtherDetailsComplete();
                    }
                    catch (Olive.Entities.ValidationException ex)
                    {
                        Notify(ex.Message, "error");
                        return View(info);
                    }
                    await new MortgageApplicationService(info.Item.Application).UpdateStatus();
 
                scope.Complete();
            }
    }
```
