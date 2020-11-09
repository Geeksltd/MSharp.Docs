# Shortcuts

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
button.Save();

// Shortcut to create:
Button("Save").OnClick(x => { x.SaveInDatabase(); x.ReturnToPreviousPage(); });
```

```csharp
button.CancelSave();

// Shortcut to the two above:
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
 return @this.Button("Save")
                .OnClick(x =>
                {
                    x.SaveInDatabase();
                    x.CloseModal(Refresh.Full);
                });
```
