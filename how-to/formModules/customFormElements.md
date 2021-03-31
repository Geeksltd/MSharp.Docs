# Custom List Control Source

## Problem

Most of the times, you create a form over an entity which you have access to all properties in that case, But sometimes you want to use a field to calculate some values on the form which you don't have in your entity. 

For example, confirm password text box. You don't need to keep that on your database but you need it on the UI level.

## Implementation

Using `CustomField()` you can add a custom element to your form.


```csharp
 CustomField().Label("Confirm new password")
                .Mandatory()
                .PropertyName("ConfirmPassword")
                .ExtraControlAttributes("type=\"password\"")
                .ViewModelAttributes("[System.ComponentModel.DataAnnotations.Compare(\"Password\",ErrorMessage=\"New password and Confirm password do not match. Please try again.\")]")
                .Control(ControlType.Textbox);

```
Using `Contorl()` you can manage the Control Type for example for adding a ReadOnly field you don't need to define Control type.

```csharp

 CustomField().Label("Name").ControlMarkup(@"@info.Item.Name");

```




