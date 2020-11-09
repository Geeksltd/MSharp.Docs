#Shortcuts

## Form Module
In a form module, you can use the following shortcut methods for typical definitions:

```csharp
button.Cancel();

// Shortcut to create:
Button("Cancel", file, line).OnClick(x => x.ReturnToPreviousPage());

```

```csharp
button.ModalCancel();

// Shortcut to create:
Button("Cancel", file, line).OnClick(x => x.CloseModal());

```
