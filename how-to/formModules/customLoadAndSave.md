# Custom data load/save


## Problem

When you use a custom element on the form, it doesn't come with any binding by default. For example, if it's a drop-down you need to set the `DataSource` for that and if you want to save the inserted value in your database you need to map that value with one of your entity properties.

## Implementation

### In the UI

For loading data, MSharp allows you to specify your data source, by using `DataSource()` on your custom element. 

```csharp
 
 CustomField().Label("Your Unit")
              .PropertyName("Unit").PropertyType("Unit")
              .DataSource("await info.GetAllUnits()")
              .ItemValueExpression("item.ID")
              .AsAutoComplete();
                
```

In this example, we load all Units into an auto complete drop down, we set their IDs as Value and their default ToString() result as Text for the drop down.

`DataSource()` accepts a string and passes this to the Controller when you build the UI.
 


For saving data, MSharp allows you to bind the data to one of your entity properties , by using `CustomDataSave()` on your custom element. 

```csharp
 
  CustomField().Label("Your Unit")
               .PropertyName("Unit").PropertyType("Unit")
               .DataSource("await info.GetAllUnits()")
               .ItemValueExpression("item.ID")
               .CustomDataSave("item.Property = info.Unit;")
               .AsAutoComplete();
                
```


 