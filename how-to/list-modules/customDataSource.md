# Custom Data Source

## Problem

By default a List will contain all records of a particular type. This is rarely the desired behaviour. You may want only the Employees from a specific Company. Maybe you want only Products purchased in July, with an Age restriction and listed in reverse alphabetical order. 

## Implementation

### In the UI

MSharp allows you to specify your data source, by using DataSource() in your list module.

```csharp
    public EmployeeList()
    {
        HeaderText("Employees")
            .DataSource("info.Employer != null ? info.Employer.Employees.GetList().Result : Employee.GetAllEmployees().Result ");

        /*
        * other code
        */

        ViewModelProperty("Company", "Employer").FromRequestParam("item");
    }

```

In this example, if Employer is known (has been passed by query string) then the DataSource() is: the Employees of that Employer. If however there is no Employer (no query string received) then the list is populated by all the Employees returned by the static method GetAllEmployees().

DataSource() accepts a string and passes this to the Controller when you build the UI.

### In the Controller

If you open the Controller you can see how the code is implemented.
If you are having difficulty forming the appropriate C# as a string it can help to formulate it in the Controller and then copy and paste it back into the Module

```csharp
    async Task<IEnumerable<Costume>> GetBaseSource(vm.CostumeList info)
    {
        IEnumerable<Costume> result = info.CachedBaseSource;

        if (result != null) return result;

        result = info.CachedBaseSource = (info.Wearer != null ? info.Wearer.Costumes.GetList().Result : Costume.GetAllCostumes().Result).ToList();

        return result;
    }
```

### Tips

In this example, if there was no Employer, the desired outcome, was that it would load all records. So this module can be used for All Employees and for Company specific Employees. It was important to ensure there were no null exceptions.

If the desired behaviour, is to display an empty list if there is no Company provided, then you can use SourceEvaluationCriteria(). If the criteria provided i.e. "info.Company != null” is not met then the DataSource is not evaluated and an empty list is produced, this prevents a null exception from occurring if the query string is not passed correctly.

Best Practice is to put any database calls or complex expressions into Methods that can be called from the Controller instead of putting them directly into DataSource().

Using .Result is important as the Controller uses async Methods.
