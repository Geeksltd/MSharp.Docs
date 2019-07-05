# Custom data source

## Problem

Sometimes in an application, you will need to be more explicit in your data source than just using the entity of the module and pulling all data from this database table. We need to be able to select which data rows we wish to use to populate a view module.

## Implementation

In M#, we have the `DataSource()` method where we can explicitly create the data source for the module.

## Example

In this example we have a `ViewModule<T>` on `Forecast`.

```csharp
using MSharp;
using Domain;

namespace Modules
{
    public class ForecastView : ViewModule<Forecast>
    {
        public ForecastView()
        {
            ViewModelProperty("DateTime?", "Filter").FromRequestParam("FilterDate");

            DataSource("await ForecastService.GetActiveAgreements(info.Filter)");

            Header("<h2>Portfolio Forecasts</h2>");

            Box("RightBox", BoxTemplate.WrapperDiv)
                .CssClass("right-box")
                .Add(
                    Field(x => x.TotalLeaseValueRemaining),

                    Field(x => x.TotalNetValue));

            Field(x => x.NumberOfActiveAgreements)
                .ItemCssClass("left-row");

            Field(x => x.TotalCustomerValueRemaining)
                .ItemCssClass("left-row");
        }
    }
}
```

This `DataSource()` uses a method in `ForecastService` called `GetActiveAgreements()` shown below.

```csharp
 public static async Task<Forecast> GetActiveAgreements(DateTime? filter)
        {
            var result = await GetActiveAssignments();
            if (result.Any())
                return result.Select(x =>
                {
                    return new Forecast
                    {
                        Customer = x.Customer,
                        TotalCustomerValueRemaining = x.EndCustomerAgreement.LeaseRental * CalculateremainingPayments(filter, x.EndCustomerAgreement.EndDate, x.EndCustomerAgreement.Frequency),
                        TotalLeaseValueRemaining = x.LeaseCompanyAgreement.LeaseRental * CalculateremainingPayments(filter, x.LeaseCompanyAgreement.EndDate, x.LeaseCompanyAgreement.Frequency),
                        NumberOfActiveAgreements = 1
                    };
                }).Aggregate((current, next) =>
                {
                    current.NumberOfActiveAgreements += next.NumberOfActiveAgreements;
                    current.TotalLeaseValueRemaining += next.TotalLeaseValueRemaining;
                    current.TotalCustomerValueRemaining += next.TotalCustomerValueRemaining;

                    return current;
                });
            return new Forecast();
```
