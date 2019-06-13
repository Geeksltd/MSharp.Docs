# Manual sorting

## Problem

Rather than sorting a list by alphabetical or numeric order.  You may wish to order a list based on the specific needs of your client.  For instance, they may have a customer that they always wish to show first on a list of customers, even though none of their property values would put them in this list position.

## Implementation

In M# we have the `SortingStatment()` method where we can specify the sort expression for the list.  This can be any C# expression using the item object.

You can have multiple sort expressions and these are separated by `|`

### Example

Lets say for example we have a simple list of customers who have a `FirstName` `LastName` and `FavouriteShoppingCategory` property

```csharp
Field(x => x.FirstName);
Field(x => x.LastName);
Field(x => x.FavouriteShoppingCategory);
```

We create a `MyModuleMethod()` that defines order based on `FavouriteShoppingCategory`  This can be any logic you wish based on the needs of your application.

We can use the following sorting statement.

```csharp
SortingStatement("MyModuleMethod(item) DESC | FirstName | LastName ")
```

This will first sort using the module method created followed by the customer's first name and then the customer's last name.
