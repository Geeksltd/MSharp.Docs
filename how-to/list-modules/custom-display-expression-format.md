# Custom display expression/format

In case you need to apply any string format on data columns you can use DisplayFormat method which will instruct M# to use String.Format on generated razor view. For more information about formatting strings please visit [String.Format Method](https://docs.microsoft.com/en-us/dotnet/api/system.string.format?view=netcore-3.1) on Microsoft Docs.



```csharp
using MSharp;
using System.Data;

namespace Modules
{
	class ProductModule : ListModule<Domain.ProductModule>
	{
		public ProductModule	{	
            Column(x => x.Title);

			Column(x => x.Description);;

            // this line will generate following razor markup:
            // <td>@(string.Format("{0:C2}", item.Price))</td>
            Column(x => x.Price).DisplayFormat("{0:C2}");

			Column(x => x.Image);
		}
	}
}
```

If you need to have a computed column you can use DisplayExpression method and pass the C# expression as the parameter. For example: 


```csharp
using MSharp;
using System.Data;

namespace Modules
{
	class ProductModule : ListModule<Domain.ProductModule>
	{
		public ProductModule	{	
            Column(x => x.Title);

			Column(x => x.Description);;

            Column(x => x.Price).DisplayFormat("{0:C2}");

            // Price plus value added tax rate of 4%
            // This line will generate the following razor markup
            // <td>@(string.Format("{0:C2}", item.Price + item.Price * 0.04))</td>
            Column(x => x.Price)
                .HeaderTemplate("Price + VAT")
                .DisplayExpression("c#:string.Format(\"{0:C2}\", item.Price + item.Price * 0.04)");
                // you can also use cs method
                //.DisplayExpression(cs("string.Format(\"{0:C2}\", item.Price + item.Price * 0.04)"));

			Column(x => x.Image);
		}
	}
}
```

> You can’t use DisplayExpression in conjunction with DisplayFormat on the same Column.