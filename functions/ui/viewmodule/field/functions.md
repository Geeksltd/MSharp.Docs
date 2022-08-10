# Field's Functions / Methods

| Function Name|Description | Samples |
|--------------|-------------|--------|
AfterControl|<br/>You can specify static contents or a C# expression which will be rendered just after the input control of the form element.<br/><br/>WHEN TO USE/SET IT?<br/>When you need to apply special design requirements.You can also use this attribute to place module buttons.|
Label|<br/>In this field you can specify the label text for this form element.<br/><br/>Note<br/>If you are manually setting this field, The system will not automatically add ":" to the end of the label.<br/>if you don't want to display a label then use [#EMPTY#] keyword<br/><br/>WHEN TO USE/SET IT?<br/>When you want to set a custom label for the form element.|
AfterControlAddon||
AfterControlContainer|<br/>You can specify static contents or a C# expression which will be rendered just after the input control container element of the form element.<br/><br/>WHEN TO USE/SET IT?<br/>When you need to apply special design requirements.You can also use this attribute to place module buttons.|
AllocateWholeRowToLabel|<br/>If set to true, the label for the element is will take the whole space (full line) and input control will be displayed on the next row underneath .<br/><br/>WHEN TO USE/SET IT?<br/>When you want to display label and input control on separate rows in block not
inline in one row|
AutoFocus|<br/>This attribute allows to to specify the auto focus behaviour of the input control Often on lengthy pages if form is below the browser normal window and control focus causes unnecessary page scroll to show the default focused element you can use this property to set the AutoFocus to False. which will prevent page to scroll on load<br/><br/>WHEN TO USE/SET IT?<br/>When you need to alter the control Auto focus|
AutoSet|<br/>Set a field value automatically|
BeforeControl|<br/>You can specify static contents or a C# expression which will be rendered just before the input control of this form element.<br/><br/>WHEN TO USE/SET IT?<br/>When you need to apply special design requirements.You can also use this attribute to place module buttons.|
BeforeControlContainer|<br/>You can specify static contents or a C# expression which will be rendered just before the input control container element of the form element.<br/><br/>WHEN TO USE/SET IT?<br/>When you need to apply special design requirements.You can also use this attribute to place module buttons.|
BeforeLabel|<br/>You can specify static contents or a C# expression which will be rendered just before the label of this form element.<br/><br/>WHEN TO USE/SET IT?<br/>When you need to apply special design requirements.|
Box|<br/>In this field you can select a box available in element section. On selecting a box, the form element will be placed inside that box.<br/><br/>WHEN TO USE/SET IT?<br/>When you need to fulfil custom design or want to group related search elements|
Control|<br/>In this field, you can select a control type from a wide range of control types for the input control e.g AutoComplete, Textbox, Checkbox List etc.<br/><br/>WHEN TO USE/SET IT?<br/>When you need to change the type of input control for the form element|
ControlCssClass|<br/>In this field, you can set a css class for this control.<br/><br/>Tips<br/>css classes should always be lower case.<br/>Use "-" to separate the words in the css class.<br/>Use " " to separate multiple css classes.<br/><br/>WHEN TO USE/SET IT?<br/>When an special appearance style is needed for the control.|
ControlWrapperCssClass|<br/>In this field, you can enter a custom css class for the wrapper of the input control.<br/><br/>Tips<br/>css classes should always be lower case.<br/>Use "-" to separate the words in the css class.<br/>Use " " to separate multiple css classes.<br/><br/>WHEN TO USE/SET IT?<br/>When you want to wrap the data entry control for a special appearance style.|
CustomDataLoad|<br/>In this field you can write a custom c# code which loads the element before data entry.<br/><br/>WHEN TO USE/SET IT?<br/>When you want to replace the default data load with custom expression for the input control.|
CustomDataSave|<br/>In this field, you can specify a C# expression which will be used to populate the related entity property when saving form data.<br/><br/>WHEN TO USE/SET IT?<br/>When you need to perform custom logic specific to UI for saving the input data especially based on custom added control on the form. Any Business logic must be written in Modal.|
CustomInitializer|<br/>In this field, you can specify a C# expression to initialize the input control. The expression specified here will be used to populate input control on page load.<br/><br/>WHEN TO USE/SET IT?<br/>In scenarios when you need to initialize the input control especially custom control added on the form.|
DisplayExpression||
DisplayFormat|<br/>In this field you can specify the format expression for this element. It is only used in ReadOnly mode.<br/><br/>WHEN TO USE/SET IT?<br/>When you want to specify a custom format expression for this element.|
ExtraControlAttributes|<br/>In this field you can specify the code to be added to the control markup.<br/><br/>Tips<br/>Use this only for values that cannot be set through the M# interface.<br/><br/>WHEN TO USE/SET IT?<br/>When you need to customize input control markup with additional attributes not available in M# .|
FormatValidationMessage||
HeaderText|<br/>In this field you can specify a static contents or C# expression which appear just above for form element container.<br/><br/>WHEN TO USE/SET IT?<br/>When you need to display contents as heading of the element.|
HelpText|<br/>In this field you can specify the instructions to show to the user for this form element.<br/><br/>WHEN TO USE/SET IT?<br/>When you need to show some instruction/help text for the form element.|
ItemCssClass|<br/>In this field, you can set a css class for this item.<br/><br/>Tips<br/>css classes should always be lower case.<br/>Use "-" to separate the words in the css class.<br/>Use " " to separate multiple css classes.<br/><br/>WHEN TO USE/SET IT?<br/>When an special appearance style is needed for the item.|
ItemsSource||
Label|<br/>In this field you can specify the label text for this form element.<br/><br/>Note<br/>If you are manually setting this field, The system will not automatically add ":" to the end of the label.<br/>if you don't want to display a label then use [#EMPTY#] keyword.<br/><br/>WHEN TO USE/SET IT?<br/>When you want to set a custom label for the form element.|
LabelCssClass|<br/>In this field, you can set a css class for this label.<br/><br/>Tips<br/>css classes should always be lower case.<br/>Use "-" to separate the words in the css class.<br/>Use " " to separate multiple css classes.<br/><br/>WHEN TO USE/SET IT?<br/>When an special appearance style is needed for the label.|
Mandatory|<br/>This attribute allows to make a form element mandatory or optional. This attribute overrides behaviour set in Modal.<br/><br/>Note<br/>If you change a form element which was marked as mandatory in Modal to optional by setting this attribute to False. Then the element will not be validated on client side but server side validation will take place as set.<br/><br/>WHEN TO USE/SET IT?<br/>When you need to make a form element mandatory on UI.|
MasterDetailCellVisibleIf||
MaximumOptions||
NoLabel|<br/>Sets the text of this element to be [#EMPTY#] which means no text should be generated.|
NoWatermarkText||
NumberOfLines||
Readonly|<br/>When set, a literal will be generated instead of a data entry control.<br/><br/>WHEN TO USE/SET IT?<br/>When you intend to just display the data for read only purposes.|
RequiredValidationMessage|<br/>In this field you can specify required field validation message for the element.<br/><br/>DEFAULT<br/>Please provide a value for [Form Element Name].<br/><br/>WHEN TO USE/SET IT?<br/>When you need to display a custom required field message.|
SkipFormGroupWrapper||
SkipGroupControlWrapper||
ToolTip|<br/>The text or markup to use for the tooltip of the control. You can use static or C# expression.<br/><br/>WHEN TO USE/SET IT?<br/>When you need to display tooltip for the form element.|
ValueExpression||
ViewModelAttributes||
VisibleIf||
WatermarkText|<br/>In this field you can specify text for watermark which hovered above the input control. This field supports both static text and C# expression.<br/><br/>Note<br/>This attribute is ignored for some of the control types e.g. Dropdown lists, Checkboxes etc.|

# Field's Events / CallBacks

| Event Name|Description | Samples |
|--------------|-------------|--------|
ChangeEventHandler|<br/>In this field you can specify a C# expression to handle the change event of the input control<br/><br/>Tips<br/>Make sure the Post back attribute is set to True<br/><br/>WHEN TO USE/SET IT?<br/>When you need to perform custom logic on change event of a form element|
ReloadOnChange|<br/>If set to True, the input control will cause postback.<br/><br/>WHEN TO USE/SET IT?<br/>When you need to enable the postback behaviour of the input control|