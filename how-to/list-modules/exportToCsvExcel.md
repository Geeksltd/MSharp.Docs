# Export to CSV or Excel

## Problem

The Client wants to be able to access the data stored in an Excel file

## Implementation

It is easy to export Lists to Excel and CSV files, simply add a button to your list module that will export the data.

You can pick ExportFormat.Csv or ExportFormat.Excel.

If you wish you can change the file name to something more appropriate using CommonActionParameter, the default is the name of the module.

```csharp

    Button("This button exports to CSV")
        .OnClick(x => x.Export(ExportFormat.Csv)
        .Set(CommonActionParameter.ExportToCsv_FileName, "My Contacts"));

    Button("This button exports to Excel")
        .OnClick(x => x.Export(ExportFormat.Excel)
        .Set(CommonActionParameter.ExportToExcel_FileName, "My Contacts"));

```

On clicking this button the User will download file “My Contacts”, this will be an excel or csv file with all the data and layout of the list visible in the browser window, including any active search filters.
