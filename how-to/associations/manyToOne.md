# Many to one relationship

## Problem

When you create applications, most of the times some of your entities are related to each other.
One of the most common relationships which you need to model is where, an instance of an entity A is related to an instance of entity B in a way that an instance of A can only be in relation to one and only one instance of B but each instance of B can be related to many instances of A.

This is called a many to one relationship from the A's side and a one to many relationship from the side of B.
we say that the relation between A to B is many to one, and B to A is one to many.
Because one instance of B can be assigned to many instances of A but each instance of A can only have a single assignment to a single instance of B.

As an example a page to book relationship is many to one from the page side since each page can only be assigned to a single book but one to many from the book side since each book can have many pages.
employee and department have a many to one relationship from the employee to department since each employee can only be in one department and from department to employee the relation is one to many since each department will have many employees.

## Implementation

Let's say we have an application recording books and their categories.
Each book has only one category and each category, obviously can be assigned to multiple books.

The relation between a book and a category, is a many to one relationship as described above.
We can use the generic `Associate<T>()` method to form the relationship.

#### ExamExample

The `Book` entity can be defined like this:

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
            Associate<Category>("Book category").Mandatory();
        }
    }
}
```

`Category` is a very simple entity for now and can be defined like this

```csharp
using MSharp;

namespace Model
{
    public class Category : EntityType
    {
        public Category()
        {
            String("Name").Mandatory();
        }
    }
}
```

The `Associate<T>()` method tells M# that each book has a property named `BookCategory` which has the type `Category`.

#### Generated Code

The generated code for the `Book` entity shows the relation as well.

```csharp
    public partial class Book : GuidEntity
    {
        CachedReference<Category> cachedBookCategory = new CachedReference<Category>();
        
       /// <summary>Gets or sets the value of Author on this Book instance.</summary>
        public string Author { get; set; }
        
        /// <summary>Gets or sets the value of Name on this Book instance.</summary>
        public string Name { get; set; }
        
        /// <summary>Gets or sets the ID of the associated Book category.</summary>
        public Guid? BookCategoryId { get; set; }
        
        /// <summary>Gets or sets the value of Book category on this Book instance.</summary>
        public Category BookCategory
        {
            get => cachedBookCategory.Get(BookCategoryId);
            set => BookCategoryId = value?.ID;
        }
}
```

Since the database table for a book now contains the ID of the category which it belongs to , it now has a `Guid` field for that and a property to get the actual category.
Also the value is cached so is only read once until the cache gets invalidated and you don't hit the database constantly.

