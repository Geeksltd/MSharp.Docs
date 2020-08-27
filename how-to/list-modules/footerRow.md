# Footer Row

## Problem

The client wants to have a footer row on a list that provides a Sum Total for the column

## Implementation

ShowFooterRow() provides a footer row for your list.

```csharp
    public ExpensesList()
    {
        HeaderText("Expenses")
            .ShowFooterRow();

        Column(x => x.Name);
        Column(x => x.Department);
        Column(x => x.Occurances)
            .FooterFormula(AggregateFormula.Max);
        Column(x => x.TotalValue)
            .FooterFormula(AggregateFormula.Sum)
            .FooterDisplayFormat("{0:C2}");

        ButtonColumn("Edit")
            .OnClick(x => x.PopUp<EnterPage>().Send("item", "item.ID"));

        Button("New Gadget")
            .OnClick(x => x.PopUp<EnterPage>());
    }

```

Having added a footer row you can now add a FooterFormula() to any column that needs a footer row value. The available formulas can be accessed using AggregateFormula and cover:

- Average
- Sum
- Max
- Min
- Count

You can change the format of your footer values using FooterDisplayFormat()
