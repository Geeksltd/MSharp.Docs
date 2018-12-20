# Bootstrap/reference data

## Problem

Usually when you create an application, you need some data in the database for different reasons including the following:

- you need some reference data to be able to test it and demo it.
- It is not wise to enter some data into the application whenever you want to do some testing.
- Sometimes you need data with specific conditions to test or need a huge amount of data for your testing.
- Some of your data might be constant from the viewpoint of the application but you still want to put it in the database and read it from there so it can be changed later on without any code changes.

For these reasons, you should be able to insert some default entities into the database when you are creating the database and M# lets you do that.

## Implementation

In the `Domain` project of your M# solution, there is a folder named `[DEV-SCRIPTS]` and inside it a code file named `ReferenceData.cs` which is designed exactly for this purpose.
M# executes this after generating the database.
You should put all of your code which creates the reference data in this class.
Let's take a look at the structure of the file first.

```csharp
    public class ReferenceData : IReferenceData
    {
        IDatabase Database;
        public ReferenceData(IDatabase database) => Database = database;

        async Task<T> Create<T>(T item) where T : IEntity
        {
            await Context.Current.Database().Save(item, SaveBehaviour.BypassAll);
            return item;
        }

        public async Task Create()
        {
            await Create(new Settings { Name = "Current", PasswordResetTicketExpiryMinutes = 2 });

            await CreateContentBlocks();
            await CreateAdmin();
        }

    ...
}
```

As you can see the class implements a specific interface which M# uses to call this after database generation.
The class's `Create()` method is called and as you see by default, an admin user and some other content is created when you create the database.
Also there is a `Create<T>(T item)` method available which allows you to create new entities and save them to the database.
Using this helper method you can create and save your own data to the database. 
Your code should be called from the `Create()` method (the one without parameters).
You usually define your `async` method which creates your entities and then call that from `Create()` to keep it clean.

### Example

Let's say we have an application to store a user's contacts.
Contacts can have different types which are known and we want to store different possible types in the database so we can show them in a dropdown to the user to choose from them.
On the other hand we don't want to make it so hard to modify the list of types so we store them as an entity in the database and insert all valid types in the `ReferenceData.cs` like this.

```csharp
public class ReferenceData : IReferenceData
    {
        IDatabase Database;
        public ReferenceData(IDatabase database) => Database = database;

        async Task<T> Create<T>(T item) where T : IEntity
        {
            await Context.Current.Database().Save(item, SaveBehaviour.BypassAll);
            return item;
        }

        public async Task Create()
        {
            await Create(new Settings { Name = "Current", PasswordResetTicketExpiryMinutes = 2 });

            await CreateContentBlocks();
            await CreateAdmin();
            await CreateContactTypes();
        }

        async Task CreateContactTypes()
        {
            await Create(new ContactType { Name = "Friend" });
            await Create(new ContactType { Name = "Family" });
            await Create(new ContactType { Name = "Business" });
            await Create(new ContactType { Name = "Other" });
        }
}
```

We define a method named `CreateContactTypes()` which creates multiple `ContactType` entities and uses the `Create<T>(T item)` method to save them to the database.
We call this `CreateContactTypes()` method in our main `Create()` method.

Now when M# generates the database and wants to create the reference data, our `ContactType` entities will be created and inserted into the database as well.

## Remarks

- This is not a good substitute for an import pipeline for a huge amount of data but can be used temporarily to run any kind of data import code If needed. However usually you want to define that process as a separate task.
- This code is a part of your development scripts and is not a part of the final application, don't put any code which you want to use at runtime here.