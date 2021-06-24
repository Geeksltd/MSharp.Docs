# Structured vs custom template

M# goal is to make developing data-focused .NET web applications as easy as possible. The key enabler for this purpose is module types in M#. You can create view components in 2 different ways in M#-based application, as explained below. 

## Structured approach
In structured mode, the intention is specified with minimal code and let the M# do its magic. Module types for this approach are shown in the following table:

| Type   |     Class     | View element |              Usage                           |
| -------|:-------------:|:------------:|:---------------------------------------------|
| Form   | `FormModule` | `Field`     |  Creating and updating an entity instance    |
| List   | `ListModule` | `Column`    | Listing entity instances of a particular type|
| View   | `ViewModule` | `Field`     | Showing a single entity instance             |
| Menu   | `MenuModule` | `Item`      | Creating menu                                |

By using any of these modules you declare view elements in each component, and then M# generate appropriate markup templates and binding code inferred from the domain model.

Using the structured approach doesn't mean you completely give up customisation. You have a lot of flexibility within this approach by further creating custom elements, styling and CSS for elements, setting button positions, changing default labels, etc.

## Custom approach
When the scenario and requirements don't fit into the structured template, you may create a custom template by specifying different pieces in the component yourself. In this approach, you can use **Markup methods** to allow you fully customise your view. These methods are discussed [here](https://www.msharp.co.uk/#/how-to/stylingAndCSS/markupCustomisation).

For modules that are not binded to an entity and view is created with `Markup` you may use `GenericModule` class.