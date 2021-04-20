- Introduction to M#

  - [What is M#?](Overview/README.md)
  - [Installing M#](Install/README.md)

- Basic M# concepts

  - [Structure of an M# solution](Structure/README.md)
  - [What is: M# Entity](Basics/Entity.md)
  - [What is: M# Page](Basics/Page.md)
  - [What is: M# Module](Basics/Module.md)

- Step-by-step tutorials

  - [Example 1: Your First App](Tutorials/1/README.md)
  - [Example 2: Modal pages, menu, etc](Tutorials/2/README.md)
  - [Your turn: Practice](Practice/readme.md)
  - [Example 3: Building a simple website](Tutorials/Building-a-simple-website/README.md)

- How-to: Model: Entity types

  - [Creating an Enum (reference) type](how-to/types/enum.md)
  - [Implementing Inheritance and abstract classes](how-to/types/inheritance.md)
  - [Creating and using Interface types](how-to/types/interfaces.md)
  - [Customizing ToString() implementation](how-to/types/customizingToString.md)
  - [Specifying default Sort order](how-to/types/sortOrder.md)
  - [Customising plural title](how-to/types/plural.md)
  - [Implementing hierarchy types](how-to/types/hierarchy.md)
  - [Implementing transient (non DB) types](how-to/types/transient.md)
  - [Adding custom methods](how-to/types/customMethod.md)

- How-to: Model: Properties

  - [Specifying the ID (primary key) property](how-to/properties/primarykey.md)
  - [Calculated vs persisted](how-to/properties/calculatedVSPersisted.md)
  - [Custom type (C#/DB)](how-to/properties/customType.md)
  - [Multi-line text](how-to/properties/multiLineText.md)
  - [Numeric scale/precision](how-to/properties/numericScaleAndPrecision.md)
  - [Nullable (int, bool, ...)](how-to/properties/nullable.md)
  - [Custom boolean text](how-to/properties/customBoolText.md)

- How-to: Model: Associations

  - [Many-to-one](how-to/associations/manyToOne.md)
  - [One-to-many](how-to/associations/oneToMany.md)
  - [Many-to-many](how-to/associations/manyToMany.md)
  - [Cascade delete](how-to/associations/deleting.md)

- How-to: Database

  - [Custom table/column name](how-to/database/customNames.md)
  - [Custom primary key](how-to/database/customPrimaryKey.md)
  - [Soft delete](how-to/database/softDelete.md)
  - [Custom data persistence](how-to/database/customPersistence.md)
  - [Index](how-to/database/index.md)
  - [Data type conversion](how-to/database/typeConversion.md)
  - [Bootstrap/reference data](how-to/database/bootstrapReferenceData.md)

- How-to: Model: Misc

  - [Name vs Title](how-to/misc/nameAndTitle.md)
  - [Notes/docs/user help](how-to/misc/NoteHelpDocumentation.md)
  - [Custom [Attributes]](how-to/misc/customAttributes.md)
  - [White-space trimming](how-to/misc/whitespaceTrimming.md)

- How-to: Validation

  - [Mandatory property](how-to/validation/mandatory.md)
  - [Numeric/date range](how-to/validation/numericAndDateRange.md)
  - [Text length](how-to/validation/textLength.md)
  - [Text pattern/regex](how-to/validation/textPatternAndRegex.md)
  - [Unique property](how-to/validation/unique.md)
  - [Uniqueness combination](how-to/validation/uniqueCombination.md)
  - [Custom validation rule](how-to/validation/customValidationRule.md)
  - [Custom pre-validation logic](how-to/validation/customPrevalidation.md)
  - [Mutually exclusive](how-to/validation/mutuallyExclusive.md)
  - [Form-specific validation](how-to/validation/formSpecificValidation.md)
  - [Custom validation message](how-to/validation/customValidationMessage.md)
  - [Delete and referential integrity](how-to/validation/referentialIntegrity.md)
  - [Allowed file extensions](how-to/validation/fileExtension.md)
  - [Form warning style](how-to/validation/warningStyle.md)

- How-to: Files & images

  - [Handling files/documents](how-to/filesAndImages/file.md)
  - [Handling images](how-to/filesAndImages/image.md)
  - [Thumbnails](how-to/filesAndImages/thumbnail.md)
  - [Image optimization](how-to/filesAndImages/optimizations.md)
  - [Default (empty) image url](how-to/filesAndImages/defaultURL.md)
  - [Secure access](how-to/filesAndImages/secureAccess.md)
  - [Custom storage](how-to/filesAndImages/customStorage.md)
  - [Displaying an image](how-to/filesAndImages/displayImage.md)
  - [Image with click action](how-to/filesAndImages/interactiveImage.md)

- How-to: Form modules

  - [Adding a textbox](how-to/formModules/addingTextbox.md)
  - [Adding a check box](how-to/formModules/addingCheckbox.md)
  - [Adding a html editor](how-to/formModules/addingHtmlEditor.md)
  - [Adding a drop down list](how-to/formModules/addingDropdownList.md)
  - [Adding a radio button list](how-to/formModules/addingRadiobuttonList.md)
  - [Adding a checkbox list](how-to/formModules/addingCheckboxList.md)
  - [Adding a date picker](how-to/formModules/addingDatePicker.md)
  - [Adding a time picker](how-to/formModules/addingTimePicker.md)
  - [Adding a date/time picker](how-to/formModules/addingDatetimePicker.md)
  - [Limiting time picker hours/minutes](how-to/formModules/limiting-time-picker-hours-minutes.md)
  - [Adding a file upload field](how-to/formModules/addingFileUploadField.md)
  - [Default values (property setter)](how-to/formModules/defaultValuesPropertySetter.md)
  - [Watermark text](how-to/formModules/watermarkText.md)
  - [Custom form elements](how-to/formModules/customFormElements.md)
  - [Custom data load/save](how-to/formModules/customLoadAndSave.md)
  - [Custom list control source](how-to/formModules/customListControlSource.md)

- How-to: Buttons/Links
  - [Adding a button](how-to/buttons-links/adding-a-button.md)
  - [Custom location for a button](how-to/buttons-links/Custom-location-for-a-button.md)
  - [Button per row](how-to/buttons-links/button-per-row.md)
  - [Multiple buttons from data source](how-to/buttons-links/multiple-buttons-from-data-source.md)
  - [Transactions](how-to/buttons-links/transactions.md)
  - [Triggering/skipping validation](how-to/buttons-links/trigering-skipping-validation.md)
  - [Default button](how-to/buttons-links/default-button.md)
  - [Button actions](how-to/buttons-links/button-actions.md)
  - [Hiding/showing buttons](how-to/buttons-links/hiding-showing-buttons.md)

- How-to: List modules
  - [Adding data column](how-to/list-modules/adding-data-column.md)
  - [Custom display expression/format](how-to/list-modules/custom-display-expression-format.md)
  - [Empty markup](how-to/list-modules/emptyMarkup.md)
  - [Adding link/button column](how-to/list-modules/adding-link-button-column.md)
  - [Adding image/icon column](how-to/list-modules/adding-image-icon-column.md)
  - [Adding input control column](how-to/list-modules/addingInputControlColumn.md)
  - [Merging columns](how-to/list-modules/merging-columns.md)
  - [Index column](how-to/list-modules/index-column.md)
  - [Select checkbox column](how-to/list-modules/selectCheckboxColumn.md)
  - [Custom column header text](how-to/list-modules/custom-column-header-text.md)
  - [User column display selection](how-to/list-modules/userColumnDisplaySelection.md)
  - [Footer row](how-to/list-modules/footerRow.md)
  - [Hiding header row](how-to/list-modules/hidingHeaderRow.md)
  - [Pagination](how-to/list-modules/pagination.md)
  - [Sorting](how-to/list-modules/sorting.md)
  - [Manual sorting](how-to/list-modules/manualSorting.md)
  - [Custom data source](how-to/list-modules/customDataSource.md)
  - [Data grouping](how-to/list-modules/dataGrouping.md)
  - [Export to CSV/Excel](how-to/list-modules/exportToCsvExcel.md)

- How-to: Search

  - [Search field on property](how-to/search/searchFieldOnProperty.md)
  - [Full text search](how-to/search/fullTextSearch.md)
  - [Instant search](how-to/search/instantSearch.md)
  - [Default search value](how-to/search/defaultSearchValue.md)
  - [Custom search element](how-to/search/customSearchElement.md)
  - Auto-search on start

- How-to: View modules
  - Custom data source
  - Structured vs custom template
  - Hiding empty elements

- How-to: Navigation
  - Custom page url
  - Auto page redirection
  - [Modal (pop-up)](how-to/navigation/modal-PopUp.md)
  - Ajax/no ajax
  - Passing and using parameters

- How-to: Menus
  - [Creating a menu](how-to/menus/creatingMenu.md)
  - Main navigation menu
  - Sub-navigation menu/tabs
  - [Dynamic menu items](how-to/menus/dynamicMenuItems.md)
  - Menu item hierarchy
  
- How-to: UI composition
  - [Visibility](how-to/uiComposition/visibility.md)
  - Module: Shared vs page-owned
  - [View components](how-to/uiComposition/viewComponents.md)
  - [Master detail forms](how-to/uiComposition/masterDetailForms.md)
  - [Merged forms](how-to/uiComposition/mergedForms.md)
  - Module references
  - [Module boxes](how-to/uiComposition/moduleBoxes.md)

- How-to: Styling and CSS
  - Standard vs custom css
  - [Mark-up customisation](how-to/stylingAndCSS/markupCustomisation.md)
  - [Header text](how-to/stylingAndCSS/headerText.md)

- How-to: Misc

  - Dependency Injection
  - [PDF generation](how-to/misc/pdfGeneration.md)
  - Page start-up logic
  - Custom module initialization
  - Custom methods in controller
  - [Custom ViewModel properties](how-to/misc/customViewModelProperties.md)
  - [Scheduled tasks](how-to/misc/scheduledTasks.md)
  - [Sending email notifications](how-to/misc/sendingEmailNotifications.md)
  - [Merging action list buttons](how-to/MergeColumns.md)
  - [Using global search](how-to/UsingGlobalSearch.md)

- How-to: Javascript
  - Custom initialization script
  - [Script to run on Button click](how-to/javascript/scriptOnButtonClick.md)

- How-to: Security

  - Authentication
  - [Role based access](how-to/security/roleBasedAccess.md)
  - Page role inheritance
  - Custom page security
  - Module specific security
  - Module visibility vs security checks
  - Sql injection
  - Parameter tampering
  - Cross site scripting
  - Web Api security
  - Form insert vs update filtering

- More Step-by-step tutorials

  - [Example 3: Uniqueness rules](Tutorials/3/README.md)
  - [Example 4: Search](Tutorials/4/README.md)
  - [Example 5: Inheritance](Tutorials/5/README.md)
  - [Example 6: Advanced Associations](Tutorials/6/README.md)
  - [Example 7: Validation and pagination](Tutorials/7/README.md)
  - [Example 8: Calculated properties](Tutorials/8/README.md)
  - [Example 9: Master-detail](Tutorials/9/README.md)
  - [Example 10: List data source](Tutorials/10/README.md)
  - [Example 11: Method logic](Tutorials/11/README.md)
  - [Example 12: Advanced validation](Tutorials/12/README.md)
  - [Example 13: Form element](Tutorials/13/README.md)
  - [Example 14: Sending email](Tutorials/14/README.md)
  - [Example 15: Formatting property](Tutorials/15/README.md)
  - [Example 16: Form wizard](Tutorials/16/README.md)
  - [Example 17: Dynamic menu](Tutorials/17/README.md)
  - [Example 18: Automated tasks](Tutorials/18/README.md)

- Structure Tutorial

  - Business Domain - Basics
    - [Understanding Entity Types](Domain/UnderstandingEntityTypes.md)
    - [Properties](Domain/Properties.md)
    - [Inheritance](Domain/Inheritance.md)
    - [Transient, Interface, Abstract](Domain/Transient.md)
    - [Generated Code](Domain/GeneratedCode.md)
    - [Partial Class & Business Logic](Domain/PartialClass.md)
    - [String Property](Domain/StringProperty.md)
    - [DateTime Property](Domain/DateTimeProperty.md)
    - [Associations](Domain/Associations.md)
    - [Number Property](Domain/NumberProperty.md)
    - [File](Domain/File.md)
    - [Boolean](Domain/Boolean.md)
    - [Calculated Properties](Domain/CalculatedProperties.md)
  - Business Domain - Advanced
    - [The role of ID](Domain/Advanced/TheRoleOfId.md)
    - [The role of IsNew](Domain/Advanced/TheRoleOfIsNew.md)
    - [The role of ToStringExpression()](Domain/Advanced/TheRoleOfToString.md)
    - [IEntity interface](Domain/Advanced/IEntityInterface.md)
    - [TransientEntity](Domain/Advanced/TransientEntity.md)
    - [MSharp Interfaces](Domain/Advanced/MSharpInterface.md)
  - Working with Data
    - [Database.Get() VS Database.Find()](Data/DatabaseGet.md)
    - [Database.GetList()](Data/DatabaseGetList.md)
    - [Database.Save()](Data/DatabaseSave.md)
    - [Database.Update()](Data/DatabaseUpdate.md)
    - [Database.Delete()](Data/DatabaseDelete.md)
    - [Database.Any(), None() and Count()](Data/DatabaseAnyNoneCount.md)
    - [ConnectionString and config](Data/ConnectionString.md)
    - [Working with existing databases](Data/WorkingWithExistingDatabase.md)
  - UI Structure
    - [Master Page](UI/MasterPage.md)
    - [Modal VS Standard](UI/ModalVSStandard.md)
    - [Module Hosting](UI/ModuleHosting.md)
    - [OnStart()](UI/OnStart.md)
    - [Page Settings](UI/PageSettings.md)

- Tips and tools
  - [Shortcut methods](Basics/shortcuts.md)
  - [Migration from legacy M#](Basics/Migration.md)
  - [VS Extensions](Basics/VSIX.md)
  - [CLI](Basics/CLI.md)
  - [Tips](Basics/Tips.md)
