* Introduction

    * [Overview](Overview/README.md)
    * [Installation](Install/README.md)
    * [Structure](Structure/README.md)
    * [Concepts](Basics/Concepts.md)

* How-to: Model: Entity types

    * Enum types
    * Inheritence (+Abstract/+DB)
    * Interface types
    * ToString()
    * Default sort
    * Plural title    
    * Hierarchy
    * Transient types
    * Custom methods

* How-to: Model: Properties

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
    * Mutually exclusive
    * Form-specific validation
    * Custom validation message
    * Delete and referrential integrity
    * Allowed file extensions

* How-to: Files & images
   
    * Handling files/documents
    * Handling images
    * Image optimization
    * Default (empty) image url
    * Secure access

* How-to: Form modules

    * Adding a textbox
    * Adding a drop down list
    * Adding a radio button list
    * ...
    * Custom form elements 
    

* How-to: List modules

    * Paging
    * Sorting
    * Manual sorting
    * Export to CSV/Excel

* How-to: View modules

* How-to: Misc
    
* How-to: Navigation

* M# Tutorials

    * [Episode 1: Your First App](Tutorials/1/README.md)
    * [Episode 2: Modal pages](Tutorials/2/README.md)
    * [Episode 3: Uniqueness rules](Tutorials/3/README.md)
    * [Episode 4: Search](Tutorials/4/README.md)
    * [Episode 5: Inheritance](Tutorials/5/README.md)
    * [Episode 6: Advanced Associations](Tutorials/6/README.md)
    * [Episode 7: Validation and pagination](Tutorials/7/README.md)
    * [Episode 8: Calculated properties](Tutorials/8/README.md)
    * [Episode 9: Master-detail](Tutorials/9/README.md)
    * [Episode 10: List data source](Tutorials/10/README.md)
    * [Episode 11: Method logic](Tutorials/11/README.md)
    * [Episode 12: Advanced validation](Tutorials/12/README.md)
    * [Episode 13: Form element](Tutorials/13/README.md)
    * [Episode 14: Sending email](Tutorials/14/README.md)
    * [Episode 15: Formatting property](Tutorials/15/README.md)
    * [Episode 16: Form wizard](Tutorials/16/README.md)
    * [Episode 17: Dynamic menu](Tutorials/17/README.md)
    * [Episode 18: Automated tasks](Tutorials/18/README.md)

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
