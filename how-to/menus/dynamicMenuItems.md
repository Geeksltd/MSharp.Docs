# Dynamic Menu Items

## Problem

You want to create Menu items dynamically that change when new content is added

For example, separate menu links go to pages that display foods which satisfy different dietary requirements. The client wants to be able to add new dietary requirements at any time and for the menu to automatically update.

## Implementation

### In the Menu Module:

```csharp
    Item("Category")
        .DataSourceType("DietType")
        .Text("c#: item.Name")
        .Key("c#: item.ID")
        .OnClick(x => x.Go<FoodsPage>().Send("category", "item.ID"));
```

-	Create a new item for your menu and give it a Name.
-	By specifying the DataSourceType() as DietType, the menu is populated with one link for every Diet Type in the database. If you do not want every instance to be used you can specify a DataSource() instead.
-	The text of the menu link will need to be written dynamically using `c#:`
-	Key is used to give each dynamically created menu link a unique identifier, which is necessary for menu item highlighting to work.
-	When you navigate using this item you must Send() the `item.ID` so you are able to generate the appropriate content on the destination page.

### Custom Menu Item Highlighting

MSharp's menu item highlighting is performed automatically by matching the urls with the menu item's link, however when using dynamic menu items you will need to add an extra rule based on the key as they all link to the same page. 
Add a SpecialSelectedKeyRule() to the Menu above its items. 

```csharp
    SpecialSelectedKeyRule("if(Request.Has(\"category\")) return Request.Query[\"category\"];");
```

This checks to see whether a query string "category" has been passed and if it has, it uses this categories value to determine what menu items Key it corresponds to.

### In the destination Module:

```csharp
    public FoodsList()
    {
        HeaderText("c#: info.Category == null ? \"Food\" : info.Category.Name")
            .SourceCriteria("info.Category == item.Category")
            .SourceEvaluationCriteria("info.Category!=null");


        ViewModelProperty("DietType", "Category")
            .FromRequestParam("category");

        /*
        * Other code
        */
    }
```

- Create a new ViewModelProperty “Category” of type “DietType” from the query string “category”.
- The header text can be made dynamic to match the menu item. Here, there is a general heading for if there is no query string received.
- The date source can be filtered using SourceCriteria(). Only items whose category matches the view model property Category will be shown.
- To avoid exceptions in the event that there is no category received, use SourceEvaluationCriteria(). If there is no info.Category then it skips SourceCriteria() and displays all results.

