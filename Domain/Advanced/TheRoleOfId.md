# The role of ID

Each data row should be unique in the system and be accessed with a reference. When you create a new Entity, M# generates by default an ID property, which is a Guid and not visible in the M# Entity editor. This ID comes from the **GuidEntity** and is used to store references to this instance in associations, or for example passing an object to another Web page using the query string.

You may want not to use it, for example if each instance can have a unique reference number, which will never change, this property could be used instead of the ID property. Please refer to [Business Domain - Basics: Lesson Properties](https://github.com/Geeksltd/MSharp.Docs/blob/master/Domain/Properties.md) part "Is primary key" for more details about the implementation.