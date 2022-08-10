# View's Functions / Methods

| Function Name|Description | Samples |
|--------------|-------------|--------|
AjaxRedirect||
AutoSet||
Box||
Button||
button|<br/>Provides a shortcut to add view buttons to this module. Equivalent to calling Button(...).|
ButtonsContainerCssClass||
ButtonsLocation||
ControllerInterfaces|<br/>The interfaces that this user control (module) should implement.<br/><br/>WHEN TO USE/SET IT?<br/>This is particularly useful when using ICallbackEventHandler interface for AJAX call backs.|
CustomAttributes||
CustomField||
DataLoadCriteria|<br/>In this field you can specify the criteria in which you want to load the data into the form.<br/><br/>WHEN TO USE/SET IT?<br/>When you want to load the data into the form only if one or more criteria are met.|
DataSource||
FindEntityType||
Footer|<br/>In this field you can specify the footer for the module.<br/><br/>WHEN TO USE/SET IT?<br/>When you want a markup to be generated at the bottom of this module.|
GenerateSaveInDatabase|<br/>If set to true, a method SaveInDatanase() will be generated which will call the Database.Save() on the instance of the form's entity type<br/><br/>Note:<br/>This attribute is ignored if any of the Supports Edit or Supports Add attribute are set to True<br/><br/>WHEN TO USE/SET IT?<br/>This is used to explicitly enforce generation of SaveInDatabase() method when both "Support Edit" and "Support Add" attributes are set to false.|
Header|<br/>The markup to add at the beginning of this module&#39;s content.<br/><br/>WHEN TO USE/SET IT?<br/>When you want a markup to be generated at the top of this module.|
HeaderText|<br/>In this field you can specify heading for the module. All contents are placed inside h2 tag.<br/><br/>WHEN TO USE/SET IT?<br/>When you wan to specify just the heading contents|
Image||
info||
Inject|<br/>Injects an instance of a specified service type.|
IsInUse|<br/>In this field you can specify if the module is used and should be build or not.<br/><br/>WHEN TO USE/SET IT?<br/>If your module is used in a page directly, it will be built in build actions automatically.<br/>If your module is not used in a page directly, but you still want it to be built, you should check this property.|
IsViewComponent||
KeepOriginalFormatting|<br/>When set to True, the generated code will not be formatted and will be generated left aligned.<br/><br/>WHEN TO USE/SET IT?<br/>It is recommended to not to set it True, because it keeping the original formatting will make it difficult to read an understand|
Link||
LoadJavascriptModule|<br/>Loads a Javascript (or Typescript) module upon page startup.|
LoadJavascriptService|<br/>Loads a Javascript (or Typescript) service upon page startup|
MarkupWrapper|<br/>In this field you can specify a wrapper template for the module.<br/><br/>WHEN TO USE/SET IT?<br/>When want to customize the appearance of the module by adding extra markup around it.|
MasterDetail||
MemberwiseClone||
MergedForm||
ModuleContentsWrapper||
Multi_Lingual|<br/>If set to True, Phrases on static phrases i.e. Label Text, Heading, columns, button texts will be translated by selected language<br/><br/>WHEN TO USE/SET IT?<br/>When you need to enable multi-lingual support on a single module. Please not that if the Multi-Lingual option in project settings is set then you do not need to set it explicitly.|
Name|<br/>In this field you should enter the name of the module you want to create. This name should be a unique name for the module you have created.<br/><br/>WHEN TO USE/SET IT?<br/>This is a mandatory field for the module.|
NamespaceImports|<br/>In this field you can choose namespace(s) you need to import in the page backend.<br/><br/>WHEN TO USE/SET IT?<br/>When you need to work with a class frequently and the namespace is not imported by default|
Orientation|<br/>In this attribute you can select the orientation of the form elements<br/><br/>WHEN TO USE/SET IT?<br/>when you need to change the orientation of the form elements|
Prefix||
Reference||
RequestParam|<br/>In this field you can specify a QueryString key which is used to retrieve the "ID" of the instance which needs to be edited on the page.<br/><br/>Tips:<br/>use QueryString Keys without prefixing with "." when you need to load an instance which will be directly consumed on the form.<br/>Prefixing QueryString keys with "." when you need to load an instance which will be used indirectly on the form e.g. in order to populate a form field<br/><br/>WHEN TO USE/SET IT?<br/>When you as using more than one forms on the page and cannot use "id" as the QueryString to load instances for both forms.|
RootCssClass|<br/>In this field you can enter the css class of the module.<br/><br/>Tips:<br/>css classes should always be lower case.<br/>Use "-" to separate the words in the css class.<br/>Use " " to separate multiple css classes.<br/><br/>WHEN TO USE/SET IT?<br/>When you need to apply some css to the module.|
SecurityChecks||
SoftError||
SupportsAdd|<br/>If set to False, The form will not support adding new instances.<br/><br/>WHEN TO USE/SET IT?<br/>When you need you form for editing purposes|
SupportsEdit||
UseAntiForgeryToken||
Using||
ValidationStyle|<br/>This attribute lets to choose the warning style(s) for validation message. You can use combination of styles.<br/><br/>WHEN TO USE/SET IT?<br/>When you need to select a different warning style for making validation warnings more sophisticated|
ViewModelInterfaces||
ViewModelProperty||
VisibleIf||
WrapInForm||

# View's Events/CallBack

| Event Name|Description | Samples |
|--------------|-------------|--------|
OnBeforeSave||
OnBound||
OnBound_GET||
OnControllerClassCode||
OnJavascript||
OnPostBound||
OnPreBinding||
OnPreBound||
OnViewModelClassCode||
OnViewModelConstructor||