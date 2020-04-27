# Multiple buttons from data source

In some situations we need to render a list of buttons or links based on a data source. These situations usually arise when we are dealing with entities which are in some association with each other.

Imagine we are developing a product catalogue for a client. We have a Product entity and ProductCategory entity as below:

```csharp

using MSharp;

namespace Domain
{
    public class Product : EntityType
    {
        public Product()
        {
            String("Name").Mandatory();
            String("Description").Mandatory();
            String("Code").Unique().Mandatory();
            Associate<Category>("Product Category").Mandatory();
        }
    }
}


```

```csharp

using MSharp;

namespace Domain
{
    public class ProductCategory : EntityType
    {
        public ProductCategory()
        {
            String("Name");
            InverseAssociate<Product>("Products", "ProductCategory").Mandatory();
        }
    }
}

```

We have created the forms and list modules for each entity and their respected pages. For the sake of argument, let’s create a details page for each category. On the details page we are going to use M#’s view model for the category entity. Here is the view model so far:

```csharp

using MSharp;

namespace Modules
{
    class CategoryViw : ViewModule<Domain.Category>
    {
        public CategoryViw()
        {
            HeaderText("Category details");
            
            Field(x => x.Name);

            Button("Back").Icon(FA.ChevronLeft).OnClick(x => x.ReturnToPreviousPage());
        }
    }
}


```

The view model simply states the name of the category and a list of buttons for all the products within this category. By clicking each button the user is going to be redirected to the Edit page of the product which we named AddOrUpdate.

Now to actually tell M# to iterate through products associated with each category we need to:
1. Chain the Button method with RepeatDataSource method
2. Provide C# expression for the data source
3. Set the name of the product as button’s text
4. Create the click workflow


```csharp

using MSharp;

namespace Modules
{
    class CategoryViw : ViewModule<Domain.Category>
    {
        public CategoryViw()
        {
            HeaderText("Category details");
            
            Field(x => x.Name);

            Button("Product")
                // item refers the current category
                .RepeatDataSource("item.Products.GetList().Result") 
                // option refers to the product, check the generated cshtml
                .Text("C#:option.Name")
                .OnClick(x=> {
                    x.Go<Admin.Products.AddOrUpdatePage>().Send("item", "option.ID").SendReturnUrl();
                });

            Button("Back").Icon(FA.ChevronLeft).OnClick(x => x.ReturnToPreviousPage());
        }
    }
}


```

> **Note**: item.Products is of type IDatabaseQuery, if you check the definition of IDatabaseQuery you’ll notice this type is not iterable, that's why we need to call GetList().