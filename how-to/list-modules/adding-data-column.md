# Adding Data Column

The default Html output of the M#’s list module is a Html table, usually we bind properties of the underlying list module’s entity to each column of the table. To bind a column to a property we use the Column method of the fluent API and pass the name of the column as an argument. Like below:

```csharp
using MSharp;
using System.Data;

namespace Modules
{
	class ProductModule : ListModule<Domain.ProductModule>
	{
		public ProductModule	{	
            Column(x => x.Title)
                .CssClass("cell-class");

			Column(x => x.Description)
                .GridColumnCssClass("column-class")
                .HeaderTemplate("<strong>Info</strong>");

            Column(x => x.Price)
                .AfterValue(" $ + ")
                .HeaderTemplate("Price + Tax");

            Column(x => x.Tax)
                .AfterValue(" $")
                .NeedsMerging();

			Column(x => x.Image);
		}
	}
}
```

To add css class to each cell of the column use the CssClass method which will wrap the content of the cell into a span element with the provided CSS class. If you like to add a css class to the td element of each row for a column use GridColumnCssClass method.

If you need to add a suffix to the data of each column you can chain the column method with the AfterValue method, remember not to use dots because the razor engine will confuse it with the dot operator. 

In rare cases on which you need to define custom markup for the header cell eg. th element use the HeaderTemplate method and pass the markup as the argument of the method.