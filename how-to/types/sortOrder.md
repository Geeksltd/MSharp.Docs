# Specifying default sort order

## Problem

Sometimes you need the entities returned from the database to be in a certain order.
M# uses the `IComparable` interface to sort entities when returning a list of them from the database.

If you care about sorting, the default implementation in `GuidEntity` is not what you want most of the times.
You want to sort your entities based on one of your defined properties.

M# always uses ascending sort order when returning entity lists from the database. 
There are times that you want to get the entities in descending order.
This is easily achievable when defining the entity as well.

## In memory or in database sorting

You can sort entities both in the database and after fetching them from the database.
We describe how to do both cases and then talk about when to use each.

## CompareTo Implementation (in memory sort after fetching)

As an example let's say we have a list of sports teams and their evaluation scores.
Each team is scored from 1 to 5 and 5 is the best score so you want to sort the teams in descending order.
You define the entities like this.

#### Example

The team is defined like this

```csharp
using MSharp;

namespace Model
{
    public class Team : EntityType
    {
        public Team()
        {
            String("Name").Mandatory();
        }
    }
}
```

And the `Rating` entity is defined like this

```csharp
using MSharp;

namespace Model.Domain
{
    public class Rating : EntityType
    {
        public Rating()
        {
            Associate<Team>("Team").Mandatory();
            var scoreProperty = Int("TeamScore").Mandatory();
            DefaultSort = scoreProperty;
            SortDescending();
        }
    }
}
```

Here we define the `TeamScore` property as the property used for sorting.
To do that we get the returned value from the `Int()` method which defines it and then assign it to `DefaultSort` property.
This will cause correct interface implementations to get generated for the entity.

Also the last line of the constructor calls `SortDescending()` which means this entity will be sorted by descending order which is what we want.
If we did not call the method or passed `false` to it then the sort was in ascending order.

#### Generated Code

Now the generated code for `Rating` implements `IComparable<T>` and `IComparable` interfaces to make correct sorting behavior based on what we requested possible.

```csharp
public partial class Rating : GuidEntity, IComparable<Rating>
    {
        CachedReference<Team> cachedTeam = new CachedReference<Team>();
        
        /* -------------------------- Properties -------------------------*/
        
        /// <summary>Gets or sets the value of TeamScore on this Rating instance.</summary>
        [System.ComponentModel.DisplayName("TeamScore")]
        public int TeamScore { get; set; }
        
        /// <summary>Gets or sets the ID of the associated Team.</summary>
        public Guid? TeamId { get; set; }
        
        /// <summary>Gets or sets the value of Team on this Rating instance.</summary>
        public Team Team
        {
            get => cachedTeam.Get(TeamId);
            set => TeamId = value?.ID;
        }
        
        
        /// <summary>Compares this Rating with another specified Rating instance.</summary>
        /// <param name="other">The other Rating to compare this instance to.</param>
        /// <returns>
        /// An integer value indicating whether this instance precedes, follows, or appears in the same position as the other Rating in sort orders.<para/>
        /// </returns>
        public int CompareTo(Rating other)
        {
            if (other is null)
                return 1;
            else
            {
                return this.TeamScore.CompareTo(other.TeamScore);
            }
        }
        
        /// <summary>Compares this Rating with another object of a compatible type.</summary>
        public override int CompareTo(object other)
        {
            if (other is Rating) return CompareTo(other as Rating);
            else return base.CompareTo(other);
        }
        
    }
```

As you can see this class implements both `IComparable` and `IComparable<T>` interfaces.
In the case of `IComparable`, it overrides the base class's implementation and in the case of `IComparable<T>` it simply implements the interface.

## ISortable interface (storing in the database in a specified order)

We can implement this interface for sorting entities when persisting them in the database.
The interface only contains an `Order` property.
To implement the interface we should call the `Sortable()` method in the entity's public constructor.

#### Example

Let's implement the `ISortable` interface for the same Rating class

```csharp
using MSharp;

namespace Model.Domain
{
    public class Rating : EntityType
    {
        public Rating()
        {
            Associate<Team>("Team").Mandatory();
            var scoreProperty = Int("TeamScore").Mandatory();
            DefaultSort = scoreProperty;
            SortDescending();
            Sortable();
            Int("Order").Mandatory();
        }
    }
}

```

Now the class generated will have an `Order` property which we can set in order to dictate the order of the object in the database.
If we want, we can make `Order` a calculated property so we calculate it based on team name and score or any other criteria.

#### Generated Code

Let's take a look at the generated code

```csharp
[EscapeGCop("Auto generated code.")]
    public partial class Rating : GuidEntity, IComparable<Rating>, ISortable
    {
        ...

        /// <summary>Gets or sets the value of Order on this Rating instance.</summary>
        public int Order { get; set; }
        
        /// <summary>Handles the Saving event of the Rating instance.</summary>
        /// <param name="e">The CancelEventArgs instance containing the event data.</param>
        async Task Rating_Saving(System.ComponentModel.CancelEventArgs e)
        {
            if (IsNew && Order == 0)
            {
                // This is a new Rating with unset Order value.
                // So set the Order property so that this Rating goes to the end of the list:
                Order = await Sorter.GetNewOrder(this);
            }
        }
        ...
    }
```

As you can see the interface is implemented and now the method for saving the data to database will take care of the cases which order is 0 and sets the value of it using the `Sorting` class's utility methods.
So if we don't set the order then the sorting will be based on the insertion time.

## Remarks

- `IComparable`'s `CompareTo()` method  is used to sort fetched items in memory and this happens regardless of the data order in the database. depending on the algorithm used sorting might be faster if the data is already sorted but you should not rely on this knowledge because, first of all the number of elements usually is low enough and secondly because it is an implementation detail of the underlying framework which might change in the future.
- Sorting the data in the database is a good idea if you need to do range queries which can be imporved by sequencial access to related data.
- As said if you always need a specific sorting criteria and you read the data a lot more than you write it, it might be a good idea to store it sorted.
- `IComparable<T>` is implemented for the convenience of the implementation of the `CompareTo()` override and is not used by M# for sorting itself.
- Most of the times you only need in memory sorting and not in database. If you are not sure, then use the in memory one.
- If you don't need sorted data, then don't waste performance by using it just because it is easy to implement.