# Entitie's Functions/Methods

| Function Name|Description | Samples |
|--------------|-------------|--------|
Abstract|<br/>If set to True, entity class definition will be amended by Abstract keyword.Abstract type entities can not be instantiated and must be inherited in order to utilize the functionality.<br/><br/>WHEN TO USE/SET IT?<br/>When you want to encapsulate generic properties and behaviours in an entity ispartial in nature and must be inherited in order to create concrete objects by extending the properties and behaviours of an entity When you want to perform Polymorphism.|
Add|<br/>|
AssignIDByDatabase|<br/>|
Associate|<br/>Adds a many to one association to the specified type.|
AssociateManyToMany|<br/>Creates a junction entity with two associations: one to this type, and one to the specified target type. It also creates an inverse association to that in this type with the specified display name and suffix of Links.|
Attributes|<br/>|
BigString|<br/>|
Bool|<br/>|
Byte|<br/>|
Cachable|<br/>If set to True, instances of the entity will be cached. All data access query will look in the cache first and then look in database tables<br/><br/>WHEN TO USE/SET IT?<br/> When you want to cache instances of the entity type having global scope in application in order to boost performance. Incorrect usage of this attribute could prove anti performance|
ClassName|<br/>|
DatabaseMode|<br/>|
Date|<br/>|
DateTime|<br/>|
Decimal|<br/>|
DismissWarning|<br/>|
Documentation|<br/>A description for the entity type to document its purpose. Make your descriptions as descriptive as possible as they will be generated as Comments above the entity definition.|
Double|<br/>|
EagerLoadData|<br/>If set to True, all the association will be loaded in the memory in one call<br/><br/>WHEN TO USE/SET IT?<br/>It should be used very carefully as it could cause performance issues. You should only set it to True, when you are sure that you will consume the child collection fetched eagerly|
ExtraClassCode|<br/>|
GenerateParseMethod|<br/> If set to True, a static method will be generated in entity class which returns the entity instance that is textually represented with a specified string value, or null if no such object is found.<br/><br/>Note<br/>- ArgumentNullException is thrown if the string argument is null or empty <br/>- The text is compared with the default property as for entity type<br/><br/>WHEN TO USE/SET IT?<br/>Usually in situations of maintaining interoperability. When dealing with XML data exchange to external system.|
GenerateUnitTests|<br/>|
GetCurrent|<br/>|
GetType|<br/>|
Guid|<br/>|
HasExternallyDomainClass|<br/>|
Implements|<br/>|
InstanceAccessors|<br/>|
Int|<br/>|
Int16|<br/>|
Int64|<br/>|
InverseAssociate|<br/>|
InverseManyToMany|<br/>|
IsEnumReference|<br/>|
IsHirarchy|<br/>|
IsInterface|<br/>|
IsRemoteCopy|<br/>|
JsonIgnore|<br/>|
LogEvents|<br/>|
MemberwiseClone|<br/>|
Money|<br/>|
Name|<br/>|
Notes|<br/>|
OpenFile|<br/>|
OpenImage|<br/>|
Percent|<br/>|
PluralName|<br/>|
PrimaryKeyType|<br/>|
Property|<br/>|
Schema|<br/>|
SecureFile|<br/>|
SecureImage|<br/>|
SoftDelete|<br/>|
Sortable|<br/>|
SortableBy|<br/>|
SortableByOrder|<br/>|
SortDescending|<br/>|
SqlSwitch|<br/>|
String|<br/>|
TableName|<br/>|
TestInstanceNameExpression|<br/>|
Time|<br/>|
ToStringExpression|<br/>|
Transient|<br/>|
UniqueCombination|<br/>|