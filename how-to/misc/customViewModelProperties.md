# Custom view model properties

## Problem

When creating a module, you may want to use data from an entity that is not the principle entity for that module.  

## Implementation

We can use `ViewModelProperty<>` to do so.  This either be something that already exists that we wish to use in this module or a new property that we only need for this particular instance.  If you are going to use a property more than once in an application, consider creating this property in the Model.

### Example

This `ViewModelProperty` is a boolean that we are creating for this single use.

```csharp
 ViewModelProperty<bool>("IsEmployed")
```

We can also call existing entities.

```csharp
ViewModelProperty<Mortgage>("Mortgage").FromRequestParam("mortgage");
```
With `FromRequestParam()` we can use an item that was passed from a previous page to use in our module.


