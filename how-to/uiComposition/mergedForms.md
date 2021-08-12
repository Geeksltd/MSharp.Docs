# Merged forms

## Problem

The client wants to create a form for an entity that has an association with another entity. The associated entity needs to be its own and separate entity and yet, its fields should be a part of this form. This scenario is known as **Merged form** where we insert the form for an associated entity along with the form for the main entity in a flattened way. In other words, the main and associated forms are merged into a single form. 

## Implementation
We can use `MergedForm` method in the form. Its usage is similar to `MasterDetail` method.


## One-to-one association example
Suppose that we have a `Property` entity that has a one-to-one association relationship with the `Address` entity as discussed [here](https://www.msharp.co.uk/#/how-to/associations/oneToOne).
We can create a `PropertyForm` that is merged with address fields.
```csharp
public class PropertyForm : FormModule<Domain.Property>
{
    public PropertyForm()
    {
        //...
        MergedForm(x => x.MainAddress, s =>
        {
            s.field.AddressLine1();
            s.field.Town();
            s.field.Postcode();
        });
    }
}
```

## Many-to-one association example
Suppose that we have a many-to-one association relationship between `Book` and `Category` entities as defined [here](https://www.msharp.co.uk/#/how-to/associations/manyToOne). We can give the user option to select one of the predefined categories shown in a drop-down control.
```csharp
public class BookForm : FormModule<Domain.Property>
{
    public BookForm()
    {
        //...
        field.BookCategory().AsDropDown();
    }
}
```
Alternatively, we can let the user insert a new category for the associated `Category` entity along with specifying the relation.
```csharp
public class BookForm : FormModule<Domain.Property>
{
    public BookForm()
    {
        //...
        MergedForm(x => x.BookCategory, s =>
        {
            s.field.Name().LabelText("Book category name");    
        });
    }
}
```
