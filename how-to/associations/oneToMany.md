# One to many relationship

## Problem

A one to many relationship is defined as a relationship where an instance of entity A can be associated with multiple instances of entity B but an instance of entity B can only have association with one instance of entity A.

For example a book is in a one to many relationship with its pages since each book can have many pages but each of those pages can only be a part of a single book.
This is useful when for example you want to get to all pages from the book, then having this one to many relationship will help you to get all of the pages which assigned the current book as their book.

## Implementation

The `InverseAssociate<T>()` method can be used to create a one to many relationship. the propert should have a many to one relationship in the other entity using the `Associate<T>()` method.
The `InverseAssociate<T>()` takes two arguments which the first one of them is the name of the property like most other property definition methods and the second one is the name of the property in the other entity which is the other side of the relation (i.e. is created using the `Associate<T>()` method).

Let's say we want to continue the example we had in the [Many to one page](manyToOne.md) and assign the relation between a book and its categories so from each category, we can find out all of the books which assigned this category to themselves.

#### Example

The `Book` entity is the same one as before 

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
            Associate<Category>("book Category").Mandatory();
        }
    }
}
```

But we need to create the relationship in the `Category` entity using the `InverseAssociate()` method.

```csharp
using MSharp;

namespace Model
{
    public class Category : EntityType
    {
        public Category()
        {
            String("Name").Mandatory();
            InverseAssociate<Book>("Book", "BookCategory").Mandatory();
        }
    }
}
```

The second argument to `InverseAssociate()` is the name of the property in the book class which shows the category of the book and is associated with `Category` entity.
Keep in mind that the name of the generated C# property should be used and not the friendly name we specify in the entity definition.
For example `"book Category"` would become `"BookCategory"`.

#### Generated Code

Thegenerated code for the `Category` entity now contains a method which loads all of  the books which have ths category from the database.

```csharp
    public partial class Category : GuidEntity
    {
        internal List<Book> cachedBook;
        
       /// <summary>Initializes a new instance of the Category class.</summary>
        public Category() => Deleting.Handle(Cascade_Deleting);
        
       /// <summary>Gets or sets the value of Name on this Category instance.</summary>
        public string Name { get; set; }
        
        /// <summary>Gets the Book of this Category.</summary>
        [Calculated]
        [XmlIgnore, Newtonsoft.Json.JsonIgnore]
        public IDatabaseQuery<Book> Book
        {
            get => Database.Of<Book>().Where(b => b.BookCategoryId == ID);
        }
}
```

There are other methods related to deleting entities with relations which will be described in the [deleting](deleting.md) page.