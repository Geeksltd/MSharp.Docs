# List's Functions / Methods

| Function Name|Description | Samples |
|--------------|-------------|--------|
AfterDataRowMarkup||
AfterFooterRowMarkup||
AfterHeaderRowMarkup||
AjaxRedirect||
AllowColumnSelection||
BeforeDataRowMarkup||
BeforeFooterRowMarkup||
Box||
Button||
button|<br/>Provides a shortcut to add view buttons to this module. Equivalent to calling Button(...).|
ButtonColumn|<br/>|
ButtonsContainerCssClass|<br/>|
ButtonsLocation|<br/>|
ButtonsLocation|<br/>|
ControllerInterfaces|<br/>The interfaces that this user control (module) should implement.<br/><br/>WHEN TO USE/SET IT?<br/>This is particularly useful when using ICallbackEventHandler interface for AJAX call backs.|
CustomAttributes|<br/>|
CustomAttributes|<br/>|
CustomField|<br/>|
CustomQueryOptions|<br/>|
CustomSearch|<br/>|
DataSource|<br/>This field is a C# expression that requires an complex type object. This object is used to display elements of the type<br/><br/>WHEN TO USE/SET IT?<br/>When you don't want to supply QueryString Key and want to specify a custom fetch object|
DisplayHeaderWhenEmpty|<br/>If set to True, the item header will always be displayed even if the data yield no record. This attribute works in junction with "Items header" attribute<br/><br/>WHEN TO USE/SET IT?<br/>When you need to display list header even if there are no records|
EmptyMarkup|<br/>The html to show when the view is empty. Use [#EMPTY#] if you don&#39;t want a system generated text.<br/><br/>WHEN TO USE/SET IT?<br/>When you want to show a custom text or markup when the view is empty.|
ExtraDataCells|<br/>|
ExtraHeaderCells|<br/>|
Field|<br/>|
field|<br/>Provides a shortcut to add view field elements to this module. Equivalent to calling Field(x => x.Property).|
Footer|<br/>In this field you can specify the footer for the module.<br/><br/>WHEN TO USE/SET IT?<br/>When you want a markup to be generated at the bottom of this module.|
Grouping|<br/>|
Header|<br/>The markup to add at the beginning of this module&#39;s content.<br/><br/>WHEN TO USE/SET IT?<br/>When you want a markup to be generated at the top of this module.|
HeaderText|<br/>In this field you can specify heading for the module. All contents are placed inside h2 tag.<br/><br/>WHEN TO USE/SET IT?<br/>When you wan to specify just the heading contents|
HideEmptyElements|<br/>If set to True, the elements which are null or empty will not be displayed|
Image|<br/>|
ImageColumn|<br/>|
IndexColumn|<br/>|
Inject|<br/>Injects an instance of a specified service type.|
IsInUse|<br/>In this field you can specify if the module is used and should be build or not.<br/><br/>WHEN TO USE/SET IT?<br/>If your module is used in a page directly, it will be built in build actions automatically.<br/>If your module is not used in a page directly, but you still want it to be built,you should check this property.|
IsViewComponent|<br/>|
ItemsHeader|<br/>In this attribute, you can specify custom markup which is displayed just above the gird header<br/><br/>WHEN TO USE/SET IT?<br/>You can use this attribute to implement any design related markup|
ItemsToFetch|<br/>In this field, you can use a static or C# expression based numeric value to specify the number of the number records needs to be fetched in DataSource. The numeric value specified here is Converted to IEnumerable.Take(Number of record) Linq expression<br/><br/>WHEN TO USE/SET IT?<br/>When you only need to fetch few records based on the requirement. This attribute is useful if used in junction with Sort Expression to.|
KeepOriginalFormatting|<br/>When set to True, the generated code will not be formatted and will be generated left aligned.<br/><br/>WHEN TO USE/SET IT?<br/>It is recommended to not to set it True, because it keeping the original formatting will make it difficult to read an understand|
Link|<br/>|
LinkColumn|<br/>|
ListContainerCssClasses|<br/>A comma separated list of css classes which will be rendered as nested container spans around the list control.<br/><br/>Tips<br/>- css classes should always be lower case.<br/>- Use "-" to separate the words in the css class.<br/>- Use " " to separate multiple css classes.<br/><br/>WHEN TO USE/SET IT?<br/>When you want to wrap your list control with a span with the specified class(es) to be able to apply a special appearance style.|
LoadJavascriptModule|<br/>Loads a Javascript (or Typescript) module upon page startup.|
LoadJavascriptService|<br/>Loads a Javascript (or Typescript) service module upon page startup.<br/><br/>Parameters<br/>serviceKey: The key used to add the service either singleton or transient. E.g. CustomService<br/>function: The method name to call on the loaded module.<br/>arguments: An argument expression to pass to the method.|
Markup|<br/>The Html which specifies the template of the object view.<br/><br/>WHEN TO USE/SET IT?<br/>When you need a custom markup for the object view that cannot be achieved only  by adding the elements to the object view.|
MarkupWrapper|<br/>In this field you can specify a wrapper template for the module.<br/><br/>WHEN TO USE/SET IT?<br/>When want to customize the appearance of the module by adding extra markup around it.|
ModuleContentsWrapper|<br/>|
Multi_Lingual|<br/>If set to True, Phrases on static phrases i.e. Label Text, Heading, columns, button texts will be translated by selected language<br/><br/>WHEN TO USE/SET IT?<br/>When you need to enable multi-lingual support on a single module. Please not that if the Multi-Lingual option in project settings is set then you do not need to set it explicitly.|
Name|<br/>In this field you should enter the name of the module you want to create. This name should be a unique name for the module you have created.<br/><br/>WHEN TO USE/SET IT?<br/>This is a mandatory field for the module.|
NamespaceImports|<br/>In this field you can choose namespace(s) you need to import in the page backend.<br/><br/>WHEN TO USE/SET IT?<br/>When you need to work with a class frequently and the namespace is not imported by default|
NoEmptyMarkup|<br/>|
PagerPosition|<br/>Pager position let's to choose the position of the pager in the list module<br/><br/>WHEN TO USE/SET IT?<br/>When you need to change the position of the pager|
PageSize|<br/>In this attribute you can specify a numeric value for the page size. This will be the number of records shown on each page of the list<br/><br/>WHEN TO USE/SET IT?<br/>When you have large number of records and want to display them in chunks using grid view paging. This helps making records view more compact rather than displaying infinite scroll bar|
PageSizeSelector|<br/>|
PagingNavigationTemplate|<br/>|
Prefix|<br/>|
Reference|<br/>|
RenderMode|<br/>This field let's you choose the server control to render the data in a list module.<br/><br/>WHEN TO USE/SET IT?<br/>When you need to display data using ListView |
RequestParam|<br/>In this field you can specify a QueryString key which is used to fetch the record from the database<br/><br/>WHEN TO USE/SET IT?<br/>When you have passed id of the entity type instance based on which you want to display the view|
RootCssClass|<br/>In this field you can enter the css class of the module.<br/><br/>Tips<br/>- css classes should always be lower case.<br/>- Use "-" to separate the words in the css class.<br/>- Use " " to separate multiple css classes.<br/><br/>WHEN TO USE/SET IT?<br/>When you need to apply some css to the module.|
RowAttributes|<br/>|
RowCssClass|<br/>|
search|<br/>Provides a shortcut to add search elements to this list module. Equivalent to calling Search(x => x.Property).|
Search|<br/>|
SearchAreaHeader|<br/>In this field you can specify custom mark which appears as the heading of the search box on a list module. The markup will be displayed only when search section contains at least one element.<br/><br/>WHEN TO USE/SET IT?<br/>When you need to display something in the header of the search box or need to implement special design requirement|
SearchBoxCssClass|<br/>In this field, you can set a css class for the search box.<br/><br/>Tips<br/>- css classes should always be lower case.<br/>- Use "-" to separate the words in the css class.<br/>- Use " " to separate multiple css classes.<br/><br/>WHEN TO USE/SET IT?<br/>When a special appearance style is needed for the element.|
SearchBoxVisibleIf|<br/>In this field you can specify the criteria in which you want the search box to be visible.<br/><br/>WHEN TO USE/SET IT?<br/>When you want the search box to be visible only if one or more criteria are satisfied|
SearchButton|<br/>|
SearchImage|<br/>|
SearchLink|<br/>|
SecurityChecks|<br/>|
SelectCheckbox|<br/>If set to true, a server side checkbox will be generated for each row to select individual row and one in the header row to select all the rows.<br/><br/>Tips<br/>- Call "GetSelectedItems()" method to get all the rows selected in backend<br/><br/>WHEN TO USE/SET IT?<br/>When you need to implement row selection in a list|
SelectCheckboxColumnIndex|<br/>In this field you can specify the index of the column in the grid view where you want to display the select checkbox for the row.<br/><br/>Note<br/>- This attribute works when Select checkbox attribute of list module is set to true<br/><br/>WHEN TO USE/SET IT?<br/>When you need to display select checkbox in a different column than the default first column|
ShowFooterRow|<br/>If set to True, a footer of the GridView will be shown<br/><br/>WHEN TO USE/SET IT?<br/>When you want a footer row to be generated on the list. |
ShowHeaderRow|<br/>If Set to False, Header row of the GridView will not be shown<br/><br/>WHEN TO USE/SET IT?<br/>When you don't want a hander row to be generated on the list.|
SoftError|<br/>|
Sortable|<br/>If set to False, columns sorting option will be disabled and a simple text header will be generated for the list<br/><br/>WHEN TO USE/SET IT?<br/>When you don't want sorting to be enabled on the header of a list especially when customized sorting formula is applied on result set or result set contains huge number of elements.|
SortingStatement|<br/>In this field you can specify the sort expression for the list.<br/><br/>Supported formats:<br/>- Property name<br/>- Any C# expression using "item" object.<br/><br/>Tips<br/>- Use \| to separate multiple sort expressions.<br/>- You can add " DESC" to the end of each phrase to specify descending sort.<br/><br/>WHEN TO USE/SET IT?<br/>When you want the items in the list to be sorted differently from the default setting of the type.|
SourceCriteria|<br/>In this field you can specify a criteria which act as a where clause for the the DataSource of the list.<br/><br/>WHEN TO USE/SET IT?<br/>When you want to filter the DataSource base on some criteria.|
SourceEvaluationCriteria|<br/>Sometimes the DataSource of a module can only be evaluated in a special condition or otherwise it will throw an exception.<br/>You can write such condition here, so that if your specified criteria is not  met, then the DataSource expression is not even evaluated.|
StartUpBehaviour|<br/>In this attribute you can select the preferred start up behaviour of the list. This affects how the result set will be loaded for the first time.<br/>Load List: List will be populated based on the specified DataSource<br/>Auto Search: List will be populated based on the specified DataSource but the<br/>DataSource will be filtered based on the search elements default set values<br/>Wait for Search: List will not be populated unless a postback happens on the page<br/><br/>WHEN TO USE/SET IT?<br/>It is a very useful attribute in situation where you have pre-set search elements and want to display results based on the search elements pre-set selected values Or, You want the user to get the results based on the search criteria.|
SupportsInserts|<br/>|
TableCssClass|<br/>In this field, you can set a css class for this grid.<br/><br/>Tips<br/>- css classes should always be lower case.<br/>- Use "-" to separate the words in the css class.<br/>- Use " " to separate multiple css classes.<br/><br/>WHEN TO USE/SET IT?<br/>When an special appearance style is needed for the grid.|
UpdateWithPost|<br/>|
UseAntiForgeryToken|<br/>|
UseDatabasePaging|<br/>|
Using|<br/>|
ViewModelInterfaces|<br/>|
ViewModelProperty|<br/>Creates a new property to be generated for this module's code.|
VisibleIf|<br/>|
WrapInForm|<br/>|
WrapListItemTemplate|<br/>If set to true, a wrapper (span element ) with the css class "list-item-wrapper" will be generated for each item<br/><br/>Tips<br/>- You can define the "list-item-wrapper" class in you css file to make the list look n feel more elegant<br/><br/>WHEN TO USE/SET IT?<br/>Set to False, When you don't want to generate the wrapper around each list item.|


# List's Events / CallBacks

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
