# Scheduled Tasks

## Problem

You want to perform a background task every day at 1 am.

For example, the Client wants to check for expired Contracts and change their Status accordingly.

## Implementation

You can create background tasks in Model > Project.cs

```csharp
    AutoTask("Check expired contracts ")
        .Every(1, TimeUnit.Day)
        .Run("await Contract.CheckExpiredContracts();");
```

This will run the task once a day. However, if you want to run the task specifically at 1 am you can run the AutoTask once an hour and only when the hour is 1, perform the associated task.

```csharp
    AutoTask("Check expired contracts")
        .Every(1, TimeUnit.Hour)
        .ExecutionCriteria("LocalTime.Now.Hour == 1")
        .Run("await Contract.CheckExpiredContracts();");
```

This code is generated in Website > app_Start > TaskManager.cs

Here, CheckExpiredContracts() is a method in Contracts that performs the required logic, as logic should not be used directly in Project.cs

```csharp
    public async static Task CheckExpiredContracts ()
    {
        var overdueContracts = await Database.GetList<Contracts>(x => x.ExpiresOn < LocalTime.Now && x.StatusId == ContractStatus.Active);

        await overdueContracts.Do(x => Database.Update(x, y => y.Status = ContractStatus.Expired));
    }
```
