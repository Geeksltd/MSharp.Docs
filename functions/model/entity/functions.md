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
InstanceAccessors|<br/>If set to True, a public static Property (accessor ) will be generated for each instance using the default property of the entity.<br/><br/>Tips<br/> - You should avoid setting this attribute when application supports globalization.<br/>- You must not set this attribute for an entity type which expects large number of records. You should<br/><br/> WHEN TO USE/SET IT?<br/> When you want to access instances of the entity type like an Enum type.|
Int|<br/>|
Int16|<br/>|
Int64|<br/>|
InverseAssociate|<br/>|
InverseManyToMany|<br/>Creates the inverse side of a two way many-to-many association.|
IsEnumReference|<br/>|
IsHirarchy|<br/>If set to True, the entity definition is extended with "IHierarchy" interface which is used to represent hierarchical data representation.<br/><br/>WHEN TO USE/SET IT?<br/> When you want to manipulate hierarchal data especially when using tree view control to render data|
IsInterface|<br/>This attribute works in junction with Transient class. If Set to True, the entity definition is "Interface".<br/><br/> Interface are best suited when you want separate the definitions of objects from their implementation.|
IsRemoteCopy|<br/>|
JsonIgnore|<br/>|
LogEvents|<br/>When set to False, no log will be generated in ApplicationEvents on saving or deleting the entity's instance<br/><br/>WHEN TO USE/SET IT?<br/>When you don't want to log events for entities hold insensitive data. It is recommended not to disable it because it is very helpful in debugging.|
MemberwiseClone|<br/> Creates a shallow copy of the current System.Object.|
Money|<br/>|
Name|<br/> In this field you specify the Name of the entity.<br/><br/>Tips<br/>- Name your entity based on the business logic while focusing on real world objects<br/>- Avoid lengthy Names meaningless names<br/>- In M#, Always write name using Sentence case with spaces and in singular form<br/><br/>Note<br/> M# will generate entities and database tables using Camel case and plural form respectively<br/><br/>WHEN TO USE/SET IT?<br/>This is a mandatory field and is required at the time of creating an entity type|
Notes|<br/>In this field you can comment any notes related to the entity regarding implementation or logic. Be as descriptive while specifying notes as possible.|
OpenFile|<br/>|
OpenImage|<br/>|
Percent|<br/>|
PluralName|<br/>In this field you can specify the plural name.|
PrimaryKeyType|<br/>|
Property|<br/>Gets a property that is already defined on this type or any of its parent types.|
Schema|<br/> In this attribute you can specify schema of the database table related to the entity. Data access code for the entity uses the scheme specified in this attribute<br/><br/> WHEN TO USE/SET IT?<br/>When you have database table schema different than the default.|
SecureFile|<br/>|
SecureImage|<br/>|
SoftDelete|<br/>When set to True, entity instance are not deleted permanently rather a special database table column [.Deleted] of type bit is marked.<br/><br/>WHEN TO USE/SET IT?<br/>When you want to keep the log of deleted data for history and debugging in the same database table|
Sortable|<br/>When set to true, Entity definition will be amended with "ISortable" interface which will enable you to persist sort order<br/><br/>Tips<br/>You must implement an int type property named "Order"<br/><br/>WHEN TO USE/SET IT?<br/>When you want to persist sort order of an entity instances which can be changed as required|
SortableBy|<br/>Does two actions in one go. 1: Marks this type as Sortable. 2: Marks the specified property as the DefaultSort of the type.|
SortableByOrder|<br/>Does 3 actions in one go. 1: Marks this type as Sortable. 2: Adds an int property named Order. 3: Marks that as the DefaultSort of the type.|
SortDescending|<br/> When set to true, the elements of then entity sequences are sorted in descending order based on the sort property specified or default property<br/><br/>WHEN TO USE/SET IT?<br/>When you want to sort elements of a sequence in descending order|
SqlSwitch|<br/>|
String|<br/>|
TableName|<br/>In this attribute, you can specify a name for the entity's database table.<br/><br/>Tips<br/>Always use Camel casing and Plural form<br/><br/>WHEN TO USE/SET IT?<br/> When you want to alter the name of the respective database table for the entity.|
TestInstanceNameExpression|<br/>In this field you can specify a C# expression which will be used to generate the text instances. The expression must yield a unique name<br/><br/>Tips<br/>- use keyword "each" to reference each instance of the entity<br/> - Follow the C# variable naming convention<br/><br/>WHEN TO USE/SET IT?<br/>When you want to generate desired text instance to make them unique and more robust|
Time|<br/>|
ToStringExpression|<br/>This is a C# expression field. You can specify the ToString expression which is used for string representation of each instance of the entity.<br/><br/>WHEN TO USE/SET IT?<br/>You want to represent each instance of the entity with a meaningful information on UI.<br/>We often use combination of properties to display an instance on UI which could become difficult to maintain afterwards if a change is required. Using this attribute you simple reference the instance and don't need to explicitly call properties and when a change is required you simply need to update this attribute.|
Transient|<br/>Sets database mode to transient.|
UniqueCombination|<br/>|