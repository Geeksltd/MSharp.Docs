# Shortcut methods

## Form Module
In a form module, you can use the following shortcut methods for typical definitions:

```csharp
button.Cancel();

// Shortcut to create:
Button("Cancel").OnClick(x => x.ReturnToPreviousPage());
```

```csharp
button.Save();

// Shortcut to create:
Button("Save")
   .OnClick(x =>
   { 
       x.SaveInDatabase(); 
       x.ReturnToPreviousPage(); 
   });
```

```csharp
button.CancelSave();

// Shortcut to the two above:
button.Cancel();
button.Save();
```

```csharp
button.Delete();

// Shortcut to create:
Button("Delete")
    .VisibleIf(CommonCriterion.IsEditMode_Item_IsNew)
    .ConfirmQuestion("Are you sure you want to delete it?")
    .OnClick(x =>
    {
        x.DeleteItem();
        x.GentleMessage("Deleted successfully.");
        x.ReturnToPreviousPage();
    });
```

```csharp
button.DeleteCancelSave();

// Shortcut to the three above:
button.Delete();
button.Cancel();
button.Save();
```

## Form Module (hosted in Modal)

```csharp
button.ModalCancel();

// Shortcut to create:
Button("Cancel").OnClick(x => x.CloseModal());
```

```csharp
button.ModalSave();

// Shortcut to create:
Button("Save")
    .OnClick(x =>
    {
        x.SaveInDatabase();
        x.CloseModal(Refresh.Full);
    });
```

## List Module
In a list module, you can use the following shortcut methods for typical definitions:

```csharp
column.Edit<MyEditPage>();

// Shortcut to create:
Button("Edit").Icon(FA.Edit).NoText()
     .HeaderText("Actions")
     .GridColumnCssClass("actions")
     .OnClick(x => x.Go<MyEditPage>().SendItemId().SendReturnUrl());
```

```csharp
button.Add<MyEnterPage>();

// Shortcut to create:
ListButton("Add").Icon(FA.Plus)
   .OnClick(x => x.Go<MyEnterPage>().SendReturnUrl());
```
