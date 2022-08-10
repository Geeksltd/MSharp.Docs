# Generic Module's Functions / Methods

| Function Name|Description | Samples |
|--------------|-------------|--------|
AjaxRedirect||
Box||
Button||
ButtonsContainerCssClass||
ButtonsLocation||
ControllerInterfaces|<br/>The interfaces that this user control (module) should implement.<br/><br/>WHEN TO USE/SET IT?<br/>This is particularly useful when using ICallbackEventHandler interface for AJAX call backs.|
CreatePhysicalModule|<br/>If this field is set to False, a separate module will not be created.<br/><br/>WHEN TO USE/SET IT?<br/>When the contents of the module are very simple |
CustomAttributes|<br/>|
DismissWarning|<br/>Dismisses all M# warnings on this object.|
FindEntityType|<br/>|
Footer|<br/>In this field you can specify the footer for the module.<br/><br/>WHEN TO USE/SET IT?<br/>When you want a markup to be generated at the bottom of this module.|
GetCurrent|<br/>|
GetType|<br/>Gets the System.Type of the current instance.|
Header|<br/>The markup to add at the beginning of this module&#39;s content.<br/><br/>WHEN TO USE/SET IT?<br/>When you want a markup to be generated at the top of this module.|
HeaderText|<br/>In this field you can specify heading for the module. All contents are placed inside h2 tag.<br/><br/>WHEN TO USE/SET IT?<br/>When you wan to specify just the heading contents|
Image|<br/>|
Inject|<br/>Injects an instance of a specified service type.|
Inject|<br/>Injects an instance of a specified service type.|
IsInUse|<br/>In this field you can specify if the module is used and should be build or not.<br/><br/>WHEN TO USE/SET IT?<br/>If your module is used in a page directly, it will be built in build actions automatically.<br/>If your module is not used in a page directly, but you still want it to be built, you should check this property.|
IsViewComponent|<br/>|
Justification|<br/>In this field you can specify the purpose of creating a generic module. Be descriptive in specifying this attribute.|
KeepOriginalFormatting|<br/>When set to True, the generated code will not be formatted and will be generated left aligned.<br/><br/>WHEN TO USE/SET IT?<br/>It is recommended to not to set it True, because it keeping the original formatting will make it difficult to read an understand|
Link|<br/>|
LoadJavascriptModule|<br/>Loads a Javascript (or Typescript) module upon page startup.<br/><br/>Parameters<br/> relativePath: The relative path of the module inside wwwroot (without extension). E.g. /scripts/CustomModule1|
LoadJavascriptService|<br/>Loads a Javascript (or Typescript) service module upon page startup.<br/><br/>Parameters<br/>serviceKey: The key used to add the service either singleton or transient. E.g. CustomService<br/>function: The method name to call on the loaded module.<br/>arguments: An argument expression to pass to the method. |
Markup|<br/>In this field you should enter the HTML body of the content. All HTML and ASP.NET tags are acceptable.<br/><br/>WHEN TO USE/SET IT?<br/>This field should be entered in order to show something in the content|
MarkupWrapper|<br/>In this field you can specify a wrapper template for the module.<br/><br/>WHEN TO USE/SET IT?<br/>When want to customize the appearance of the module by adding extra markup around it.|
MemberwiseClone|<br/>Creates a shallow copy of the current System.Object.|
ModuleContentsWrapper|<br/>|
Multi_Lingual|<br/>If set to True, Phrases on static phrases i.e. Label Text, Heading, columns, button texts will be translated by selected language<br/><br/>WHEN TO USE/SET IT?<br/>When you need to enable multi-lingual support on a single module. Please not that if the Multi-Lingual option in project settings is set then you do not need to set it explicitly.|
Name|<br/>In this field you should enter the name of the module you want to create. This name should be a unique name for the module you have created.<br/><br/>WHEN TO USE/SET IT?<br/>This is a mandatory field for the module.|
NamespaceImports|<br/>In this field you can choose namespace(s) you need to import in the page backend.<br/><br/>WHEN TO USE/SET IT?<br/> When you need to work with a class frequently and the namespace is not imported by default |
Prefix|<br/>|
Reference|<br/>|
RootCssClass|<br/>In this field you can enter the css class of the module.<br/><br/> Tips<br/>- css classes should always be lower case.<br/>- Use "-" to separate the words in the css class.<br/>- Use " " to separate multiple css classes.<br/><br/>WHEN TO USE/SET IT?<br/>When you need to apply some css to the module.|
SecurityChecks|<br/>|
SoftError||
UseAntiForgeryToken|<br/>|
Using|<br/>|
ViewModelInterfaces|<br/>|
ViewModelProperty|<br/>Creates a new property to be generated for this module's code.|
VisibleIf|<br/>|
WrapInForm|<br/>|
# Generic Module's Events / CallBacks

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

