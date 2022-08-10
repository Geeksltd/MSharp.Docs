# Properties's Functions/Methods

| Function Name|Description | Samples |
|--------------|-------------|--------|
Accepts|<br/>Use this field to use an alternative text patterns for the text fields in the model. These patterns affect the appearance, behaviour and validation rules for this field.<br/>The available options are:<br/>- Email address<br/>- Internet URL<br/>- ...<br/><br/>WHEN TO USE/SET IT?<br/>Use this attribute to specialised text fields to one of the options above.|
Async|<br/>|
Attributes|<br/>In this field you can specify custom C# attribute(s) for the property.<br/><br/>WHEN TO USE/SET IT?<br/>When you need to apply custom C# attributes on the property.|
Calculated|<br/>If set to True, the property is only generated in Modal entity class and no respective  column is generated in database table<br/><br/>WHEN TO USE/SET IT?<br/>When you need to generate calculated properties especially when you need to display the value on UI|
CalculatedFrom|<br/>Sets this property to calculated. Also sets its getter expression.|
ColumnName|<br/>|
CSharpTypeName|<br/>|
DatabaseIndex|<br/>If set to True, database index is generated for the property. Index are created to boost up the speed of data retrieval but downgrades the data writing speed if used unnecessary.<br/><br/>WHEN TO USE/SET IT?<br/>When the property is going to be used rigorously to retrieve data from the database.|
DatabaseType|<br/>|
Default|<br/>In this field you can specify a static or c# expression based value which is et as the default value of the property in entity class constructor<br/><br/>WHEN TO USE/SET IT?<br/>When you want to specify a default vale for a property|
DefaultFormatString|<br/>In this field you can specify the string format for a property which will be used to format the string on UI.<br/><br/>WHEN TO USE/SET IT?<br/>It is useful in cases of specifying a default format for DateTime and Numeric value to be printed on the screen using a default format string.|
DismissWarning|<br/>Dismisses all M# warnings on this object.|
Documentation|<br/>In this field you can specify contents which are generated in the documentation summary tag of the poetry<br/><br/>WHEN TO USE/SET IT?<br/>It is good practice to provide documentation of properties to make it more useable for consumer of the property or the developer who are going to manipulate it later on.|
Exposed|<br/>|
FormatValidationMessage|<br/>|
GetCurrent|<br/>|
Getter|<br/>In this field you can specify a C# expression to implement the get accessory of a calculated property<br/><br/>WHEN TO USE/SET IT?<br/>When you have a calculated property and want to implement custom get accessor|
GetType|<br/>Gets the System.Type of the current instance.|
HashPassword|<br/>Use this property if you wish to store the password fields values encrypted/hashed in your database.<br/>This will make your application more secure, since you do not store the passwords in the database in clear format<br/><br/>Note<br/>You will not be able to recover the user passwords anymore, you only can reset hashed passwords.<br/><br/>WHEN TO USE/SET IT?<br/>Additional level of security.|
HelpText|<br/>In this property you can specify contends which are displayed as the help text for the property. This property is also available in form module<br/><br/>WHEN TO USE/SET IT?<br/>When you need to display a dynamic help text property which requires Business Logic. Use Form Module element attribute "help text " to specify static help text with html markup.|
IsPrimaryKey|<br/>|
IsReadOnlyInterfaceProperty|<br/>If set to True, only the get accessor will be generated.<br/><br/>WHEN TO USE/SET IT?<br/>This is useful in scenarios when you want to have field which needs to be initialized at runtime time which should not be changed. Although, Constant variables are used as well but they cannot have dynamic value or initialized at runtime|
IsRowVersion|<br/>|
JsonIgnore|<br/>|
Lines|<br/>Specifies the number of lines to use for the textboxes when rending the forms for this element on this entity.  By default, every text field will be displayed in a control, but if you enter a number larger than 1, then it will be rendered as a TextArea field.<br/><br/>WHEN TO USE/SET IT?<br/>In order to convert a text field to a TextArea in the forms.|
Mandatory|<br/>If set to True, a required validation rule will be generated in Modal and a required field validation control will be generated on UI to require the input.<br/>This behaviour can be overridden in UI using same attribute of form element. But, if the property is marked as mandatory the rule will be applied in modal even if it is set to false in UI<br/><br/>WHEN TO USE/SET IT?<br/>When you need to make a field mandatory for an entity instance|
Max|<br/>Specifies the capacity of this String property. In other word, the maximum number of characters which could be saved in this field. The application will generate an error message if you try to save an string longer that the value entered here in this field.<br/><br/>WHEN TO USE/SET IT?<br/>In case you want to save values with larger string sizes or smaller ones.|
MinLength|<br/>|
Name|<br/>In this Property you specify the name of the property which is generated in Modal to access this property.<br/><br/>Note<br/>- Specify unique name in the entity<br/>- Specify name in Camel case e.g. ResidenceAddress, ProductBatch, IsAllowed etc.<br/><br/>WHEN TO USE/SET IT?<br/>It is a mandatory property|
NeedsDatabaseTypeConversion|<br/>|
Notes|<br/>A description for the property to document any notes. Make your descriptions as descriptive as possible as they will be helpful later on to understand the Business Logic.|
Override|<br/>If set to true, Override keyword will be generated for the property<br/><br/>WHEN TO USE/SET IT?<br/>When you have defined a virtual property in the base class and want to override the property in the derived class|
RequiredValidationMessage|<br/>In this field you can specify a message which is displayed when the property value is null<br/><br/>WHEN TO USE/SET IT?<br/>When you need to display a dynamic validation message which requires business logic.|
SaltProperty|<br/>|
Setter|<br/>|
Title|<br/>In this Property you specify the title of the property which is generated as the label in the module.<br/><br/>Note<br/>- Specify unique name in the entity<br/>- Specify name in normal case e.g. Residence address, Product batch, Is allowed?<br/><br/>WHEN TO USE/SET IT?<br/>It is a mandatory property|
TrimValues|<br/>A Boolean field to specify whether the model should trim the string values, removing empty spaces at the beginning and the end of the string, before saving it into database.<br/><br/>WHEN TO USE/SET IT?<br/>By default, M# trims all string values. If you want to change this behaviour, you have to set it to false.|
Unique|<br/>If set to True, a unique validation rule for this property will generated in the Modal which will prevent duplicate values.<br/>Also, a static method will be generated which finds and retunes an instance from the database by the property's value The method name is inferred from the property name. e.g Marking a property "Email" as unique will generate a method "FindByEmail"<br/><br/>WHEN TO USE/SET IT?<br/>Use this attribute when you want to make a property value unique|
Virtual|<br/>If set to True, "Virtual" keyword will be generated in the property definition<br/><br/>WHEN TO USE/SET IT?<br/>When you are defining a base class and want to override this property in derived classes|
XmlIgnore|<br/>When set to True, the property will not be serialized when xml serialization will be performed on the instance<br/><br/>WHEN TO USE/SET IT?<br/>When you need to perform XML serialization and When you want to omit the property value|


