# Referential Integrity

## Problem

Referential integrity is a property in databases where , if a table references another table using a foreign key, the record in the other table surely exists and the data is never incomplete/incorrect.
This is something which is usually enforced in relations by choosing what to do when we want to delete an entity which is refered to from other tables.
There are multiple possiblities and M# allows us to exactly choose what will happen.

## Implementation

The `OnDelete()` method of the associations which we create by using `Associate<T>()` method allows us to set the desired behavior so the refrential integrity of the data is always preserved.

The different possible behaviors are:

- `SetToNull` will set the related foreign key to null so a foreign key to a none-existing record is no longer available in our table. This is useful for the cases which it is allowed for the relation to be null/none-existing
- `CascadeDelete` means all related entities will be deleted. This is useful for the cases that all related entities are not meaningful without the relation like students of a deleted school or books of a deleted author.
- `ThrowWarning` This means , the system will not allow the data to be deleted because other tables are referring to it. This is useful for the cases that some relation should not be deleted unless no other table is referring to it like products in a sale which should sell a limited number of them. We should not delete the sale unless all products are sold (your sales manager won't like this statement).
- `CallReleaseXXX` means a method with the name `ReleaseXXX()` will be called for custom behavior where XXX is the name of the association's property. The delete will happen unless you throw an exception.

For more information and an example of how to use `OnDelete()` to preserve referential integrity, see [cascade delete page](how-to/associations/deleting.md).