# Specifying default sort order

M# always uses ascending sort order when returning entity lists from the database. 
There are times that you want to get the entities in descending order.
This is easily achievable when defining the entity.

## Implementation

As an example let's say we have a list of sports teams and their evaluation scores.
Each team is scored from 1 to 5 and 5 is the best score so you want to sort the teams in descending order.
You define the score entity like this.

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

And the scores entity is defined like this

```csharp
using MSharp;

namespace Model.Domain
{
    public class Score : EntityType
    {
        public Score()
        {
            Associate<Team>("Team").Mandatory();
            Int("TeamScore").Mandatory();
            DateTime("Month").Mandatory();
            SortDescending();
        }
    }
}
```

The last line of the constructor calls `SortDescending()` which means this entity will be sorted by descending order which is what we want.

## Remarks

