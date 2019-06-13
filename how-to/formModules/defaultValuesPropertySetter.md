# Default values (property setter)

## Problem

There will be times in your applications where you have a property that you wish to have a default value for if that property does not have a value.

## Implementation

We can set a default value in the model using the M# `Default()` method.  Here we can pass whatever we would like the default for this property to be.

This can be useful for doing things such as setting a non-mandatory field as "unknown" as a default or setting a `DateTime` property to `LocalTime.Now` as default.

### Example

Below is an example of a property that has a default value of `LocalTime.Now`.

```csharp
DateTime("Created on").Mandatory().Default("c#:LocalTime.Now");
```

This means that when this entity is created, `The DateTime` will be set to the time that the entity was created.

Another example shows how we can even set the default value for an associated entity

```csharp
Associate<Status>("Status").Mandatory().Default("FirstStatus");
```

This means that your status will always be set to the first status when you create the entity.
