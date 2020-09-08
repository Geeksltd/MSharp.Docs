# Module Boxes

## Problem

You have a form with a lot of required information. For improved usability you want to subdivide the form into sections.

For example, for a new Customer form you may need contact details, billing details, delivery details and preferences

## Implementation

You can use Module Boxes to display the data in separate sections. 

Start by creating a new Box variable. This box will require a Name, used as the Header where appropriate, and a BoxTemplate.

There are a few built in Box Templates that you can use depending on your needs.
-	WrapperDiv - When necessary for styling, try using with CssClass().
-	Header Box - Simply adds a header to your sections.
-	Collapsible Panel - The user can expand or collapse the section by clicking the Header
-	Tabs - The User can display one tabbed box at a time by clicking tabs

Having created a Box you can add any elements you want to it using Box().

```csharp
    var contactBox = Box("Contact Details", BoxTemplate.Tabs);

    Field(x => x.Name).Box(contactBox);
    Field(x => x.PhoneNumber).Box(contactBox);
    Field(x => x.EmailAddress).Box(contactBox);

    var deliveryBox = Box("Delivery Details", BoxTemplate.Tabs);

    Field(x => x.Address).Box(deliveryBox);
    Field(x => x.Postcode).Box(deliveryBox);

    var billingBox = Box("Billing Details", BoxTemplate.Tabs);

    Field(x => x.CardNumber).Box(billingBox);
    Field(x => x.ExpiryDate).Box(billingBox);
    Field(x => x.AccountName).Box(billingBox);

    var preferencesBox = Box("Preferences", BoxTemplate.HeaderBox);

    Field(x => x.WantsEmail).Box(preferencesBox);
```

Laying it out this way is not necessary, but is advisable. Boxes are generated in the same order they are declared and fields that are not in a box will be displayed first. 

### Nesting

Boxes can be nested using NestedBoxes()

```csharp
    var outerBox = Box("Outer Box", BoxTemplate.HeaderBox);
    var nestedBox = outerBox.NestedBox("Nested One", BoxTemplate.HeaderBox);
    var secondNestedBox = outerBox.NestedBox("Nested Two", BoxTemplate.HeaderBox);
```

Elements can be added to either of the these three boxes, but elements added to outerBox will be displayed after the nested boxes.
