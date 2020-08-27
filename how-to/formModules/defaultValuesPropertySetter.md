# Default Values (Property Setter)

## Problem

You want a form to be prepopulated with information from the previous page. For example, you follow a link from an Employee page to a Task form and you want the Employees details already filled in.

## Implementation

Property setting allows you to give default values to fields on a form populated with information passed to the page when you load it. The field remains editable so the User can change this value if they wish.

First you need to send the information to the form page. So, if you were coming from a List you may have a ButtonColumn that looks like this:

```csharp
    ButtonColumn("Add")
        .HeaderText("Tasks")
        .GridColumnCssClass("actions")
        .OnClick(x => x.PopUp<EnterPage>()
        .Send("employee", "item.ID"));

```

Send() passes a query string, called "employee" with the Item ID of the list item, to the EnterPage.

Now you need to tell the destination form how to use this information.

```csharp

    public TaskForm()
    {
        HeaderText("Task");


        Field(x => x.Employee).AsDropDown(); 
        Field(x=> x.CompletionDate).AsDatePicker() 
        Field(x => x.Description).NumberOfLines(5);

        Button("Cancel").OnClick(x => x.CloseModal());

        Button("Save").IsDefault().Icon(FA.Check)
            .OnClick(x =>
            {
                x.SaveInDatabase();
                x.GentleMessage("Saved successfully.");
                x.CloseModal(Refresh.Ajax);
            });

        AutoSet(x => x.Employee).FromRequestParam("employee");
    }
```

AutoSet() tells the form that the Employee field should automatically be set to the value given by the query string “employee”.

If there is no query string with the name “employee”, the field will remain unset. This can happen if you come from a different source page that doesn’t provide an employee or if you have not referred to the query string by the same name in both locations.

Other methods on AutoSet include:

- OnlyIf() – Property setting will only occur if the given criteria are met
- Value – Use a C# expression instead of a query string
