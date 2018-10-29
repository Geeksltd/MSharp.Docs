# Warning Style

## Problem

When users enter some data in a form and the data is invalid in one way or another, we usually want to tell them what was wrong with the enterd data and help them to fix it.

There are multiple ways to show these types of warnings and M# allows you to choose how to display them to the users.
There are multiple things to consider like the size of the warning and what your users are used to, number of elements in the form and ... but regardless of what you will choose for your application, it should be both easy to do and change later on which M# makes possible.

## Implementation

When you implement your form modules, you can define the warning style which the form uses.
`FormModule<IEntity>` class which form modules inherit from, contains a `ValidationStyle()` method which takes an array of `WarningStyle` enum and combines all of those styles to show the warnings of the form.

`WarningStyle` enum contains the following values as options which can be combined together as well.

- `AfterControl` Shows the warning after the control of the form field
- `AfterLabel` Shows the warning after the label of the form field
- `BeforeControl` Shows the warning before the control of the form field
- `BeforeLabel` Shows the warning before the label of the form field
- `MessageBox` Shows the warning as a message box
- `SummaryBlock` shows the warning in a block
- `Tooltip` Shows the warning as a tooltip

