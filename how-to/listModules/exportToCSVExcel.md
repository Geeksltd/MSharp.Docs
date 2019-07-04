# Export to CSV/Excel

## Problem

There will be times in an application when you will want the user to be able to export the contents of a list as a comma separated value (CSV) file.  This type of file can be opened in Excel and the user can view, manipulate and print out the data in its list format from here.

## Implementation

In M# we have the `Export()` method that allows us to export data from a list on a click event.  We can choose the export format of the data.

## Example

In this example we have chosen the CSV export format.

```csharp
Button("Export").OnClick(x =>
            {
                x.Export(ExportFormat.Csv)
            });
```

This creates the following code in the controller.

```csharp
public async Task<ActionResult> Export(vm.AdviserCaseNotesList info)
{
    try
    {
        return await ExportAs(info, Olive.Export.Format.Csv);
    }
    catch (Exception ex)
    {
        return Notify(ex.Message, "error");
    }
}
```
