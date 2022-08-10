# Menu's Functions / Methods

| Function Name|Description | Samples |
|--------------|-------------|--------|
AjaxRedirect||
Box||
Button||
ButtonsContainerCssClass||
ButtonsLocation||
ControllerInterfaces|<br/>The interfaces that this user control (module) should implement.<br/><br/>WHEN TO USE/SET IT?<br/>This is particularly useful when using ICallbackEventHandler interface for AJAX call backs.|
CustomAttributes|<br/>|
DismissWarning|<br/>Dismisses all M# warnings on this object.|
ExtraTagAttributes|<br/>You can set special attributes in this field. M# generates an asp.net menu control with all the attributes specified here<br/><br/>Tips<br/>- Use this only for values that cannot be set through the M# interface.<br/>- Set "Generate Links" attribute to false in order to use this attribute<br/><br/>WHEN TO USE/SET IT?<br/>When you want to add a custom attribute to asp.net menu control.|
FindEntityType|<br/>|
Footer|<br/>In this field you can specify the footer for the module.<br/><br/>WHEN TO USE/SET IT?<br/>When you want a markup to be generated at the bottom of this module.|
GenerateLinks|<br/>If set to False, an asp.net Menu control will be generated with menu items.<br/><br/> WHEN TO USE/SET IT?<br/>When you need use dynamic asp.net menu control with custom DataSource and menu item binding|
GetCurrent|<br/>|
GetType|<br/>Gets the System.Type of the current instance.|
Header|<br/>The markup to add at the beginning of this module&#39;s content.<br/><br/>WHEN TO USE/SET IT?<br/>When you want a markup to be generated at the top of this module.|
HeaderText|<br/>In this field you can specify heading for the module. All contents are placed inside h2 tag.<br/><br/>WHEN TO USE/SET IT?<br/>When you wan to specify just the heading contents|
Image|<br/>|
Inject|<br/>Injects an instance of a specified service type.|
IsInUse|<br/>In this field you can specify if the module is used and should be build or not.<br/><br/>WHEN TO USE/SET IT?<br/>If your module is used in a page directly, it will be built in build actions automatically.<br/>If your module is not used in a page directly, but you still want it to be built, you should check this property.|
IsViewComponent|<br/>|
Item|<br/>|
ItemLayout|<br/>In this attributer you specify customize the menu item makeup<br/><br/>Tips<br/>- Use "[#Link#]" as a placeholder for the generated link.<br/>- Use this only in "Generate Links" mode.<br/><br/>WHEN TO USE/SET IT?<br/>When you need style the menu items for special appeared or need to display custom contents around the menu options|
ItemTemplate|<br/>In this field you can specify the template for all menu items of this menu.<br/><br/>Tips<br/>- Use "[#ITEM#]" as a placeholder for the generated link.<br/>- Use this only in "Generate Links" mode.<br/><br/>WHEN TO USE/SET IT? <br/>When you want to specify the template for all menu items of this menu.|
KeepOriginalFormatting|<br/>When set to True, the generated code will not be formatted and will be generated left aligned.<br/><br/>WHEN TO USE/SET IT?<br/>It is recommended to not to set it True, because it keeping the original formatting will make it difficult to read an understand|
Link|<br/>|
LoadJavascriptModule|<br/>Loads a Javascript (or Typescript) module upon page startup.<br/><br/>Parameters:<br/>relativePath: The relative path of the module inside wwwroot (without extension). E.g. /scripts/CustomModule1<br/>staticFunctionInvokation: An expression to call [a static method] on the loaded module.|
LoadJavascriptService|<br/>Loads a Javascript (or Typescript) service module upon page startup.<br/><br/>Parameters:<br/>serviceKey: The key used to add the service either singleton or transient. E.g. CustomService<br/>function: The method name to call on the loaded module.<br/>arguments: An argument expression to pass to the method.|
MarkupWrapper|<br/>In this field you can specify a wrapper template for the module.<br/><br/>WHEN TO USE/SET IT?<br/>When want to customize the appearance of the module by adding extra markup around it.|
MemberwiseClone|<br/>Creates a shallow copy of the current System.Object.|
ModuleContentsWrapper|<br/>|
Multi_Lingual|<br/>If set to True, Phrases on static phrases i.e. Label Text, Heading, columns, button texts will be translated by selected language<br/><br/>WHEN TO USE/SET IT?<br/>When you need to enable multi-lingual support on a single module. Please not that if the Multi-Lingual option in project settings is set then you do not need to set it explicitly.|
Name|<br/> In this field you should enter the name of the module you want to create. This name should be a unique name for the module you have created.<br/><br/>WHEN TO USE/SET IT?<br/>This is a mandatory field for the module.|
NamespaceImports|<br/>In this field you can choose namespace(s) you need to import in the page backend.<br/><br/>WHEN TO USE/SET IT?<br/>When you need to work with a class frequently and the namespace is not imported by default |
Orientation|<br/>In this field you can set the orientation of the menu items. which can be horizontal or vertical.<br/><br/>WHEN TO USE/SET IT?<br/>When you need to change the orientation of menu options to vertical|
Prefix|<br/>|
Reference|<br/>|
RootCssClass|<br/>In this field you can enter the css class of the module.<br/><br/>Tips<br/>- css classes should always be lower case.<br/>- Use "-" to separate the words in the css class.<br/> - Use " " to separate multiple css classes.<br/><br/>WHEN TO USE/SET IT?<br/>When you need to apply some css to the module.|
SecurityChecks|<br/>|
SoftError|<br/>|
SpecialSelectedKeyRule|<br/>A C# statement that returns a string value specifying the key of the selected item based on a special criteria.<br/>That value will be matched with the "Key" attribute of every menu item and will highlight the matched item as selected (by adding css class of "selected" to that item).<br/><br/>WHEN TO USE/SET IT?<br/>If you have any dynamic menu items in this menu, for properly highlighting the correct item, a correct expression should be specified here.|
SubItemBehaviour|<br/>|
UlCssClass|<br/>|
UseAntiForgeryToken|<br/>|
Using|<br/>|
ViewModelInterfaces|<br/>|
ViewModelProperty|<br/>Creates a new property to be generated for this module's code.|
VisibleIf|<br/>|
WrapInForm|<br/>|

# Menu's Events / Callbacks

| Event Name|Description | Samples |
|--------------|-------------|--------|
OnBound||
OnBound_GET||
OnControllerClassCode||
OnJavascript||
OnPostBound||
OnPreBinding||
OnPreBound||
OnViewModelClassCode||
OnViewModelConstructor||
