# Custom column header text

## Problem

Sometimes when creating a list (especially with custom columns), the name of the column may need to be different from the name of the property that will be populating that column.

## Implementation

We can use the `LabelText()` method to create a new header by passing a string.

## Example

```csharp
CustomColumn(x => x.Name).LabelText("Subscription type");
 ```

 In this example, instead of showing the column name as "Name" it will show in the table as "Subscription type"

![Subscription types](images/subscriptionTypes.PNG)
