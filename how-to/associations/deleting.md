# Cascading deletes

## Problem

When entities have relations with each other, deleting them has consequences on other entities.
For example if you have a set of shops which sell books and you delete a book from your list, then shops which have that book should do something about it.
Depending on your business logic you might want to do different things like not allowing a book to be deleted unless no shops has any copy of it, or deleting the book from all shop listings as well.
M# allows you to decide on this per relation.

## Implementation

The `OnDelete()` method can be used on the relation to tell M# what to do with the entity when a delete operation of the association is taking place.
For example if you define this in your `Book` entity `Associate<Category>("Book category").Mandatory().OnDelete(CascadeAction.ThrowWarning)`, you are defining what to do with book entities when the category assigned to them is being deleted.

`CascadeAction` can have the following values

- `ThrowWarning` (default value) Means the association cannot be deleted until an entity associated with it exists. This is the default behavior. In the example above, the category cannot be deleted unless no books with the category exist.
- `SetToNull` sets all associated columns/properties to `null`. In the example above, all those books which their category got deleted, set their category to `null`.
- `CascadeDelete` means all associated entities will be deleted as well. In the example above, if you delete a category, all books which had that category will be deleted as well.
- Call `ReleaseXXX()` method will call a method named `ReleaseXXX()` where XXX is the name of your association's property. In the above example it would be `ReleaseBookCategory()` and you should define it in your `Book` entity's logic in a partial class.

Let's take a look at an example that when we delete the category, all books with the category will be deleted.

#### Example

Here is our `Book` entity:

```csharp
using MSharp;

namespace Model
{
    public class Book : EntityType
    {
        public Book()
        {
            String("Name").Mandatory();
            String("Author").Mandatory();
            Associate<Category>("book Category")
                .Mandatory()
                .OnDelete(CascadeAction.CascadeDelete);

            InverseManyToMany<Shop>("Shops", "Books");
        }
    }
}
```

The `Category` entity is same as before:

```csharp
using MSharp;

namespace Model
{
    public class Category : EntityType
    {
        public Category()
        {
            String("Name").Mandatory();
            InverseAssociate<Book>("Book", "BookCategory")
                .Mandatory();
        }
    }
}
```

As you can see in the `Associate()` call chain in the book entity, we called the `OnDelete()` method and assigned `CascadeDelete` to it as the behavior.

#### Generated Code

The code for `Category` is generated like this

```csharp
    public partial class Category : GuidEntity
    {
...

        /// <summary>Initializes a new instance of the Category class.</summary>
        public Category() => Deleting.Handle(Cascade_Deleting);
        
        /// <summary>Handles the Deleting event of this Category.</summary>
        /// <param name="source">The source of the event.</param>
        /// <param name="e">The CancelEventArgs instance containing the event data.</param>
        async Task Cascade_Deleting()
        {
            // Cascade delete the dependant Book:
            await Database.Delete(await Book.GetList());
        }

        ...
    }
```

As you can see, we set the delete event to be handled by the `Cascade_Delete()` method. The `Cascade_Delete()` method deletes all books with this category.