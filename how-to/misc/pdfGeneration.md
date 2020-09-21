# PDF Generation

## Problem

The Client wants to generate a PDF with information from the website

## Implementation

### Set Up PDF Capability

First you will need to install wnvhtmlconvert on the Domain project. MSharp does not currently support version 15 so use version 14.


In the Domain, add a utility class for PDFs which contains the following code:

```csharp
using Olive;
using Winnovative;
using Olive.PDF;

namespace Domain
{
    public class Html2PdfConverter : HtmlToPdfConverter, IHtml2PdfConverter
    {
        public Html2PdfConverter()
        {
            LicenseKey = Config.Get("Olive.Html2Pdf:LicenseKey");
        }
        
        public byte[] GetPdfFromUrlBytes(string url) => ConvertUrl(url);
    }
}
```

Next, add the following to appsettings.json - You will need to obtain a valid license key

```csharp
  "Olive.Html2Pdf": {
    "LicenseKey": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "ConverterType": "Domain.Html2PdfConverter, Domain"
  }
```

### Create a PDF

Start by making a page that features all your required content in the same way as you would make a normal webpage. The html from this page is used to make the PDF.

```csharp
    public ProductPDFPage()
    {
        Roles(AppRole.Local_Request, AppRole.Admin);
        Layout(Layouts.PDF);
        Add<Modules.ProductView>();
    }
}
```

-	It is important that you enable access by local_Request
-	It is advisable to create a suitable PDF Layout
-	Add modules as you would to a normal page

To generate the PDF, navigate to this page in the usual way but add a PDFFileName().

```csharp
            ButtonColumn("Download PDF")
                .Icon(FA.Download)
                .OnClick(x => x.Go<ProductPDFPage>()
                    .SendItemId().
                    PdfFileName("ProductDetails"));
```

Now, when this button is clicked instead of navigating to the webpage it will download a PDF of it.
