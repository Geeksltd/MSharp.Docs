# Column's Functions / Methods

| Function Name|Description | Samples |
|--------------|-------------|--------|
AfterValue|<br/>|
AsAutoComplete|<br/>Sets the control of this element to AutoComplete| Sets the control of this element to AutoComplete.|
AsCalendar|<br/>|
AsCheckBox|<br/>|
AsCheckBoxes|<br/>This method may cause the controls to be generated as selectable cards id you pass image/icon or explicitly say so.|
AsCollapsibleCheckBoxList|<br/>|
AsDateAndTimePicker|<br/>|
AsDatePicker|<br/>|
AsDropDown|<br/>|
AsFileUpload|<br/>|
AsHtmlEditor|<br/>|
AsListbox|<br/>|
AsNumericUpDown|<br/>|
AsRadioButtons|<br/>This method may cause the controls to be generated as selectable cards id you pass image/icon or explicitly say so.|
AsSlider|<br/>|
AsSwitch|<br/>|
AsTextbox|<br/>|
AsTimePicker|<br/>|
Box|<br/>In this field, you can select the box which you want this view element to be moved. You must first create at least a box in the boxes section and then set it here.<br/><br/>WHEN TO USE/SET IT?<br/>When you want to group a number of view elements in different box/containers in the same view. For example, you can create a box named "Address" and then put fields like "Street", "City", Country", and "Post Code" inside that box.|
CellVisibleIf|<br/>|
ColumnRepeatSource|<br/>|
Control||
ControlAttributes|<br/>|
CssClass|<br/>In this field, you can set a css class for this element.<br/><br/>Tips<br/>- css classes should always be lower case.<br/>- Use "-" to separate the words in the css class.<br/>- Use " " to separate multiple css classes.<br/><br/>Note<br/>- For List elements (columns) when the Render mode is set to "Grid", use the "Grid column css class" property to set a css class for the column.<br/><br/>WHEN TO USE/SET IT?<br/>When an special appearance style is needed for the element.|
DataSource|<br/>|
DismissWarning|<br/>Dismisses all M# warnings on this object.|
DisplayExpression|<br/>The html (could be dynamic) to display the item in this element.<br/><br/>Note<br/>- If left empty the appropriate field will be added.<br/>Supports:<br/>1. HTML tags<br/>2. Server tags<br/><br/>WHEN TO USE/SET IT?<br/>When you want to use an alternative control for a field, or create a complex  markup for a field.|
DisplayFormat|<br/>You can specify the display format which you want to use for displaying the value of this field here. This field is useful when you want to display a Numerical, or DateTime value in a certain format. The display format string must use Composite Formating and be compatible with format strings you would use in String.Format Method.<br/><br/>WHEN TO USE/SET IT?<br/>When you want to display the value of a field in a format other than standard format.|
DisplayMode|<br/>This field works only in List Module<br/>This property sets the visibility options of a column in a list module. If at least one column in a list has a display mode value other than default, then it would become possible for the users to select the columns they would like to see in the list.<br/>There are four possible options for this attribute:<br/>1. Always: means this column must be always visible and users can not hide it<br/>2. Default: the default behaviour means it will be visible, but users can hide it<br/>3. Selectable: means this column will be initially hidden, but users can make it visible<br/>4. Hidden: means this column will be hidden and users will not be able to make it visible.<br/><br/>WHEN TO USE/SET IT?<br/>If you set the Display mode of one single columns, you will change the behaviour of the whole module.<br/>Use this field when you have too many columns in a list view and want to make the visibility of some of the columns optional.|
EmptyMarkup|<br/>Use this field to specify what should be displayed when the value for this field is empty. This is especially useful for highlighting missing data in a View or List module.<br/><br/>WHEN TO USE/SET IT?<br/>When you want some expression to be displayed when the value of a field is empty.|
ExcelTemplate|<br/>This field only works on List Module Element Specifies an alternative output format when this field is exported to Excel. By default every field is exported to Excel as it is displayed on the screen. This field allows you to use an alternative format for the Excel file.<br/><br/>WHEN TO USE/SET IT?<br/>Use this when you one to specify a different format string for the field when it&#39;s formatted to Excel.|
ExportToExcel|<br/>This field only works on List Module Element  A Boolean value to specify if you want this field to be included when exporting the list to Excel file.<br/><br/>WHEN TO USE/SET IT?<br/>If you do not wish a certain column to be exported to Excel |
ExportToExcelRule|<br/>|
FooterDisplayFormat|<br/>This field only Works on List Module Element This attribute is used along with the FooterFormula. Use this attribute to specify the format for the value you specified in the FooterFormula. This attribute uses the Composite Formatting Numeric Format Strings.<br/><br/>WHEN TO USE/SET IT?<br/>Use this when you want to format the result of the FooterFormula in a certain format.|
FooterFormula|<br/>This field only Works on List Module Element<br/> You can use this attribute to specify a formula to be displayed for a column at the footer row of a list.<br/>The possible formulas are:<br/>- Average<br/>- Sum<br/>- Max<br/>- Min<br/>- Count<br/>Note<br/>You can use this in combination with FooterDisplayFormat.<br/><br/>WHEN TO USE/SET IT?<br/>Use this value to specify a formula for the footers.|
FooterMarkup|<br/>This field only Works on List Module Element<br/>The markup to appear in the footer of the element in the list.<br/><br/>Notes<br/>- This markup is only rendered if "Footer row" is checked on the list.<br/><br/>WHEN TO USE/SET IT?<br/> When you want to add a custom markup for the footer of the list.|
GetCurrent|<br/>|
GetProperty|<br/>|
GetType|<br/>Gets the System.Type of the current instance.|
GridColumnCssClass|<br/>This field only Works on List Module Element<br/>In this field, you can set a css class for this grid.<br/><br/>Tips<br/>- css classes should always be lower case.<br/>- Use "-" to separate the words in the css class.<br/>- Use " " to separate multiple css classes.<br/><br/>WHEN TO USE/SET IT?<br/>When an special appearance style is needed for the grid.|
HeaderTemplate|<br/>This attribute works only on List Module Element<br/>The markup to appear in the header template of the element in the list. List elements including button and custom elements are placed inside tag of the grid view control. Markup / Template specified in this field will be places in of the respective tag<br/><br/>WHEN TO USE/SET IT?<br/>When you want to add a custom markup for the footer of the element in the list.|
HelpText|<br/>|
IsSortable|<br/>This field works only on List Module element<br/>This field specifies if this field in the list is going to be sortable or not.<br/><br/> WHEN TO USE/SET IT?<br/>For custom columns, or columns where being sortable does not make sense. For example columns that contain a button.|
ItemCssClass|<br/>|
LabelText|<br/>In this field you can specify the label text for this element.<br/><br/>Note<br/> - If you are manually setting this field, The system will not automatically add  ":" to the end of the label.<br/>- if you don't want to display a label then use [#EMPTY#] keyword<br/><br/>WHEN TO USE/SET IT?<br/>When you want to set a custom label for the element.|
MergeUp|<br/>A shortcut to set NeedsMerging and SeperatorTemplate. Relevant to List modules only (in grid style).|
NeedsMerging|<br/>This field only works on List Module Element<br/>If set to True, the element column will be merged in the previous column and both elements are shown in one heading<br/><br/>WHEN TO USE/SET IT?<br/>When you need to display two elements in one column of the list|
NoLabelText|<br/> Sets the label text of this element to be [#EMPTY#] which means no text should be generated.|
SeperatorTemplate|<br/>This field only works on list Module Element when the "Render mode" is set to List<br/>This is field you can specify html markup to be displayed as the separator of list items on UI<br/><br/>WHEN TO USE/SET IT?<br/>When you need to apply special appended styles|
SoftError|<br/>|
SortingStatement|<br/>This field on works for list Module Element<br/>Use this field if you want to specify a sort statement for this element other than the default sort statement.<br/><br/>Tips<br/>- Use "\|" to separate multiple sort expressions.<br/>- You can add " DESC" to the end of each phrase to specify descending sort.<br/><br/>WHEN TO USE/SET IT?<br/>When you want the items in the list to be sorted differently from the default setting of the type based on this element. For example when you have a custom column that combines multiple values but you want it to be sortable based on a certain formula.|
SortKey|<br/>This field only works on List Module Element<br/>In this attribute you can specify a sort key for the list element header.<br/><br/>WHEN TO USE/SET IT?<br/>When you want to enable sorting or want to apply same key for other elements or want to make it unique|
ViewModelAttributes|<br/>|
ViewModelName|<br/>An ID for when you want to specify an exact identifier for the controller you want to use in this view element.<br/>This field is usually used in combination with ControlType to use a control type other than the Text for the view element control.<br/><br/>WHEN TO USE/SET IT?<br/>When you want to access a control from your code behind in order to get or set a value, you can specify a ControlID to find that control.|
ViewModelType|<br/>In this field, you can specify the alternative control type you wish to use for this field.<br/><br/>WHEN TO USE/SET IT?<br/>When you want to use a control other than the Literal control for a field.|
VisibleIf|<br/>|

# Column's Events / CallBacks

| Function Name|Description | Samples |
|--------------|-------------|--------|