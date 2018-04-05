# IEntity interface

All M# entities implement `IEntity`. This interface contains the property `IsNew` (more details [here](https://github.com/Geeksltd/MSharp.Docs/blob/master/Domain/Advanced/TheRoleOfIsNew.md)), the method `Validate()` which is called for validating your object, and the function `GetId()` which returns the ID of the Entity (more details [here](https://github.com/Geeksltd/MSharp.Docs/blob/master/Domain/Advanced/TheRoleOfId.md)).

```C#
namespace Olive.Entities
{
    //
    // Summary:
    //     Represents an M# Entity.
    public interface IEntity : IComparable
    {
        //
        // Summary:
        //     Determines whether this object has just been instantiated as a new object, or
        //     represent an already persisted instance.
        bool IsNew { get; }

        //
        // Summary:
        //     Creates a new object that is a copy of the current instance.
        //
        // Returns:
        //     A new object that is a copy of this instance.
        IEntity Clone();
        //
        // Summary:
        //     Gets the id of this entity.
        object GetId();
        //
        // Summary:
        //     Invalidates all its cached referencers.
        [EditorBrowsable(EditorBrowsableState.Never)]
        void InvalidateCachedReferences();
        //
        // Summary:
        //     Validates this instance and throws ValidationException if necessary.
        Task Validate();
    }
}
```