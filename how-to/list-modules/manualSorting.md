# Manual Sorting

## Problem

The Client wants the User to be able to change the order of list Items

## Implementation

### Make The Entity Sortable
First, go to the Model and make the entity sortable. 
To make an entity sortable you must do 3 things:
- Make the Entity implement ISortable
- Give it an integer Property called Order
- Make this property the DefaultSort

Fortunately, if you make the entity SortableByOrder(), MSharp will do all this for you.

```csharp
    public Product()
    {
        SortableByOrder();

        String("ID Number").Mandatory().Unique();
        String("Weight in kg");
        String("Description");
        Associate<ProductCategory>("Category").Mandatory();
    }
```

The values of Order are written as multiples of 10, so the first item will have order 10 and the second, order 20. This gap allows the program to reorder items.

### Add A Sorting Column

Now you can add a sorting LinkColumn to the List Module in the UI.

```csharp
    LinkColumn("Sort")
        .GridColumnCssClass("actions")
        .HeaderText("Sort")
        .NoText()
        .Icon(FA.Sort)
        .OnClick(x => x.DragSort());
```
Of note:
-	You must use a LinkColumn not a ButtonColumn
-	OnClick() adds the functionality DragSort() to the links. 
-	It will not function without NoText()

The order is persisted with Ajax calls, it’s not affected by refreshing the page

### Order Siblings

So far you have applied an Order to all records in the database, so every record has a unique Order. However, if you only ever see a subset of the entity you may only require the Order to be unique for each subset.

To do this, add a method GetSiblings() to the Domain Logic for your Entity.
```csharp
    public Task<IEnumerable<Product>> GetSiblings()
    {
        return Category.Product.GetList();
    }
```

This method must:

-	be called GetSiblings
-	be public
-	return a Task which returns an Enumerable of your Entity

If this method exists MSharp will automatically use it to only apply unique order to siblings.

This means that if you have 2 products in the same Category, they would have orders 10 and 20, but a third Product in a different Category would also have order 10.

Doing this, means that only the subset gets reordered, not the whole database, reducing loading times.
