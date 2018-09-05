* Introduction to M#

    * [What is M#?](Overview/README.md)
    * [Installing M#](Install/README.md)        
    
* Basic M# concepts

    * [Structure of an M# solution](Structure/README.md)
    * [What is: M# Entity](Basics/Entity.md)
    * [What is: M# Page](Basics/Page.md)
    * [What is: M# Module](Basics/Concepts.md)
    
* Step-by-step tutorials

    * [Example 1: Your First App](Tutorials/1/README.md)
    * [Example 2: Modal pages](Tutorials/2/README.md)
    * [Example 3: Uniqueness rules](Tutorials/3/README.md)

* How-to: Model: Entity types

    * Creating an Enum (reference) type
    * Implementing Inheritence *(TODO: Include Abstract and DB mode)*
    * Creating and using Interface types
    * Customising ToString() implementation
    * Specifying default Sort order
    * Customising plural title
    * Implementing hierarchy types
    * Implementing transient (non DB) types
    * Adding custom methods

* How-to: Model: Properties

    * Specifying the ID (primary key) property
    * Calculated vs persisted    
    * Custom type (C#/DB)
    * Multiline text
    * Numeric scale/precision
    * Nullable (int, bool, ...)
    * Custom boolean text
    
* How-to: Model: Associations

    * Many-to-one
    * One-to-many
    * Many-to-many
    * Cascade delete


* How-to: Database

    * Custom table/column name
    * Custom primary key
    * Soft delete
    * Custom data persistence
    * Index
    * Data type conversion
    * Bootstrap/reference data

* How-to: Model: Misc

    * Name vs Title
    * Notes/docs/user help
    * Custom [Attributes]
    * White-space trimming
    
* How-to: Validation

    * Mandatory property    
    * Numeric/date range
    * Text length
    * Text pattern/regex
    * Unique property
    * Uniqueness combination
    * Custom validation rule
    * Custom pre-validation logic
    * Mutually exclusive
    * Form-specific validation
    * Custom validation message
    * Delete and referrential integrity
    * Allowed file extensions
    * Form warning style

* How-to: Files & images
   
    * Handling files/documents
    * Handling images
    * Thumbnails
    * Image optimization
    * Default (empty) image url
    * Secure access
    * Custom storage
    * Displaying an image 
    * Image with click action

* How-to: Form modules

    * Adding a textbox
    * Adding a check box
    * Adding a html editor
    * Adding a drop down list
    * Adding a radio button list
    * Adding a checkbox list
    * Adding a date picker
    * Adding a time picker
    * Adding a date/time picker
    * Limiting time picker hours/minutes
    * Adding a file upload field
    * Default values (property setter)
    * Watermark text
    * Custom form elements 
    * Custom data load/save
    * Custom list control source
    
* How-to: Buttons/Links

    * Adding a button
    * Custom location for a button
    * Button per row
    * Multiple buttons from data source
    * Transactions
    * Trigerring/skipping validation
    * Default button
    * Button actions
    * Hiding/showing buttons
    

* How-to: List modules

    * Adding data column
    * Custom display expression/format
    * Adding link/button column
    * Adding image/icon column
    * Adding input control column
    * Merging columns
    * Index column
    * Select checkbox column
    * Custom column header text
    * User column display selection
    * Footer row
    * Hiding header row
    * Paging
    * Sorting
    * Manual sorting
    * Custom data source
    * Data grouping
    * Export to CSV/Excel
    
 * How-to: Search
 
    * Search field on property
    * Full text search 
    * Instant search
    * Default search value
    * Custom search element
    * Auto-search on start

* How-to: View modules
    * Custom data source
    * Structured vs custom template
    * Hiding empty elements

   
    
* How-to: Navigation

    * Custom page url
    * Auto page redirection
    * Modal (pop-up)
    * Ajax/no ajax
    * Passing and using parameters
    

* How-to: Menus
    * Creating a menu
    * Main navigation menu
    * Sub-navigation menu/tabs
    * Dynamic menu items
    * Menu item hierarchy
    * Current menu item highlighting    
    
    
* How-to: UI composition
    * Visibility
    * Module: Shared vs page-owned
    * View components
    * Master detail forms
    * Merged forms
    * Module references
    * Module boxes
    
    
* How-to: Styling and CSS

    * Standard vs custom css
    * Mark-up customisation
    * Header text
    

* How-to: Misc

    * PDF generation
    * Page start-up logic
    * Custom module initialization
    * Custom methods in controller
    * Custom view model properties
    * Scheduled tasks
    * Sending email notifications
    
* How-to: Javascript
    * Custom initialization script
    * Script to run on Button click
    
* How-to: Security

    * Authentication
    * Role based access
    * Page role inheritence
    * Custom page security
    * Module specific security
    * Module visibility vs security checks
    * Sql injection
    * Parameter tampering
    * Cross site scripting
    * Web Api security
    * Form insert vs update filtering
    

* More Step-by-step tutorials

    * [Example 4: Search](Tutorials/4/README.md)
    * [Example 5: Inheritance](Tutorials/5/README.md)
    * [Example 6: Advanced Associations](Tutorials/6/README.md)
    * [Example 7: Validation and pagination](Tutorials/7/README.md)
    * [Example 8: Calculated properties](Tutorials/8/README.md)
    * [Example 9: Master-detail](Tutorials/9/README.md)
    * [Example 10: List data source](Tutorials/10/README.md)
    * [Example 11: Method logic](Tutorials/11/README.md)
    * [Example 12: Advanced validation](Tutorials/12/README.md)
    * [Example 13: Form element](Tutorials/13/README.md)
    * [Example 14: Sending email](Tutorials/14/README.md)
    * [Example 15: Formatting property](Tutorials/15/README.md)
    * [Example 16: Form wizard](Tutorials/16/README.md)
    * [Example 17: Dynamic menu](Tutorials/17/README.md)
    * [Example 18: Automated tasks](Tutorials/18/README.md)

* Structure Tutorial

    * Business Domain - Basics
      * [Understanding Entity Types](Domain/UnderstandingEntityTypes.md)
      * [Properties](Domain/Properties.md)
      * [Inheritance](Domain/Inheritance.md)
      * [Transient, Interface, Abstract](Domain/Transient.md)
      * [Generated Code](Domain/GeneratedCode.md)
      * [Partial Class & Business Logic](Domain/PartialClass.md)
      * [String Property](Domain/StringProperty.md)
      * [DateTime Property](Domain/DateTimeProperty.md)
      * [Associations](Domain/Associations.md)
      * [Number Property](Domain/NumberProperty.md)
      * [File](Domain/File.md)
      * [Boolean](Domain/Boolean.md)
      * [Calculated Properties](Domain/CalculatedProperties.md)
    * Business Domain - Advanced
      * [The role of ID](Domain/Advanced/TheRoleOfId.md)
      * [The role of IsNew](Domain/Advanced/TheRoleOfIsNew.md)
      * [The role of ToStringExpression()](Domain/Advanced/TheRoleOfToString.md)
      * [IEntity interface](Domain/Advanced/IEntityInterface.md)
      * [TransientEntity](Domain/Advanced/TransientEntity.md)
      * [MSharp Interfaces](Domain/Advanced/MSharpInterface.md)
    * Working with Data
      * [Database.Get() VS Database.Find()](Data/DatabaseGet.md)
      * [Database.GetList()](Data/DatabaseGetList.md)
      * [Database.Save()](Data/DatabaseSave.md)
      * [Database.Update()](Data/DatabaseUpdate.md)
      * [Database.Delete()](Data/DatabaseDelete.md)
      * [Database.Any(), None() and Count()](Data/DatabaseAnyNoneCount.md)
      * [ConnectionString and config](Data/ConnectionString.md)
      * [Working with existing databases](Data/WorkingWithExistingDatabase.md)
    * UI Structure
      * [Master Page](UI/MasterPage.md)
      * [Modal VS Standard](UI/ModalVSStandard.md)
      * [Module Hosting](UI/ModuleHosting.md)
      * [OnStart()](UI/OnStart.md)
      * [Page Settings](UI/PageSettings.md)

* Tips and tools

    * [CLI](Basics/CLI.md)
    * [Tips](Basics/Tips.md)
