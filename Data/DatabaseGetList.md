# Database.GetList\<T\>()

This method within M# Data access repository returns a list of records `IEnumerable<T>` for a specific Entity `T`. . M# gives you the possibility to get a list of data from the database and to apply filters. Below are the codes of the overloads for this method:

### OverLoads

```C#
namespace Olive.Entities
{
    public interface IDatabase
    {
        //... other methods

        Task<IEnumerable<T>> GetList<T>(Expression<Func<T, bool>> criteria = null) where T : IEntity;

        //... other methods
    }
}
```

### Examples
```C#
var users = Database.GetList<User>();

var users = Database.GetList<User>(x=>x.Email.Contains("@geeks.ltd.uk"));
```