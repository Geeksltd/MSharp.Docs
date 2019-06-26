# Custom data persistence

## Problem

Sometimes your data is stored in an external database so you  have to connect to that database to read/modify it.
It might be accessed using a REST API or stored in another database of your company.

sometimes it is already in a database table in your SQL Server database and you don't want the M# code generator to generate database tables for you.

You still want the DAL code and entity code but not the table generation queries.
It might be the case that the data for the table is imported or is migrated from an old version of the application or ...

M# handles both cases

## Implementation

The case of creating entity code and DAL code is very easily handled by setting the entity's `DatabaseMode()` to `Existing`.
Then M# will not generate the SQL queries for creating the table for you.
You just need to be careful to set correct table and column names for your entity.

However connecting to external data sources is more involved and you need to do the following:

- Set `DatabaseMode()` of the entity to `Custom`
- Implement `IDataProvider` for your external data source
- register your data provider in `AppSettings.json` so it is used when trying to do database CRUD operations on the entity type

The interface you need to implement is provided here

```csharp
public interface IDataProvider
    {
        string ConnectionStringKey { get; set; }
        Type EntityType { get; }
        IDataAccess Access { get; }
        string ConnectionString { get; set; }

        Task<object> Aggregate(IDatabaseQuery query, AggregateFunction function, string propertyName);
        Task BulkInsert(IEntity[] entities, int batchSize);
        Task BulkUpdate(IEntity[] entities, int batchSize);
        Task<int> Count(IDatabaseQuery query);
        Task Delete(IEntity record);
        Task<int> ExecuteNonQuery(string command);
        Task<object> ExecuteScalar(string command);
        Task<IEntity> Get(object objectID);
        //
        // Summary:
        //     Returns a direct database criterion used to eager load associated objects.
        DirectDatabaseCriterion GetAssociationInclusionCriteria(IDatabaseQuery masterQuery, PropertyInfo association);
        Task<IEnumerable<IEntity>> GetList(IDatabaseQuery query);
        IDictionary<string, Tuple<string, string>> GetUpdatedValues(IEntity original, IEntity updated);
        string MapColumn(string propertyName);
        string MapSubquery(string path, string parent);
        //
        // Summary:
        //     Reads the many to many relation and returns the IDs of the associated objects.
        Task<IEnumerable<string>> ReadManyToManyRelation(IEntity instance, string property);
        Task Save(IEntity record);
        bool SupportValidationBypassing();
    }
```
