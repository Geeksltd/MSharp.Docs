# Database.Any(), None(), Count()

In this lesson, we will learn about very useful extension method on `IEnumerable` type.

## Any\<T\>()

#### Overloads

This method has two overloads and is used with conditional statements where we need to check if the resulting sequence is not empty.

```csharp
namespace Olive.Entities
{
    public interface IDatabase
    {
        //... other methods

        Task<bool> Any<T>() where T : IEntity;

        Task<bool> Any<T>(Expression<Func<T, bool>> criteria) where T : IEntity;       

        //... other methods
    }
}
```

#### Examples

The first overload of this method doesn't require any criteria / condition and is used just to determine if a sequence holds any elements, as shown below:

```csharp
if (await Database.Any<Employee>())
{
    // Perform business logic
}
```

The second overload requires a condition statement and determines if any element of a sequence satisfies the condition. The supplied condition can contain any number of logical operators.

```csharp
if (await Database.Any<Employee>(e => e.IsActivated))
{
    // Perform business logic
}
```

## None\<T\>()

This method has also two overloads and is also used with conditional statements where we need to check if the resulting sequence is empty.

#### Overloads

```csharp
namespace Olive.Entities
{
    public interface IDatabase
    {
        //... other methods
       
        Task<bool> None<T>() where T : IEntity; 

        Task<bool> None<T>(Expression<Func<T, bool>> criteria) where T : IEntity;      

        //... other methods
    }
}
```
#### Examples

The first overload of this method doesn�t require any criteria / conditions and is used just to determine if sequence holds no elements, as shown below:

```csharp
if (await Database.None<Employee>())
{
    // Perform business logic
}
```

The second overload requires a condition statement and determines if a sequence contains no elements which satisfy the condition. The supplied condition can contain any number of logical operators.

```csharp
if (await Database.None<Employee>(e => e.IsActivated))
{
    // Perform business logic
}
```

## Count\<T\>()

This method is used to determine the number of elements in any sequence and must be used only with expression.

#### Overload

```csharp
Task<int> Count<T>(Expression<Func<T, bool>> criteria) where T : IEntity;
```

#### Example

```csharp
if (await Database.Count<Employee>(e => e.IsActivated) > 5)
{
    // Perform business logic
}
```


