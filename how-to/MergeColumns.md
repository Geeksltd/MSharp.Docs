# Merging Columns

By default **M#** generate each action button to a seperate table cell. For instance, here you can see we have 5 action buttons that consume large space:

![1](https://user-images.githubusercontent.com/1321544/46538501-16b4ef80-c8c1-11e8-8570-3c2ea3991f59.PNG)

If you need to merge these action buttons to a one drop-down list button you should open `bower.json` and update `olive.mvc` package to the latest version.
After updating `olive.mvc` package all action buttons which have `.actions` CSS class would be merged into a single cell and their action title would be merged too.

![2](https://user-images.githubusercontent.com/1321544/46538813-cdb16b00-c8c1-11e8-9f07-a1cf75289079.PNG)

![3](https://user-images.githubusercontent.com/1321544/46538827-d99d2d00-c8c1-11e8-83e3-bc95a0862ca5.PNG)

In the more complex scenario, you may need to just merge some of the buttons and not all of them. As you can see in this picture, we need two separate action buttons and other actions should be merged:

![4](https://user-images.githubusercontent.com/40687782/46793408-8ef63780-cd3d-11e8-977b-39ae786a54dc.png)

To generate this, you just need to change the title and the class of the two actions buttons and let other actions buttons have `actions` CSS class:

```csharp
 ButtonColumn("Action A").HeaderText("Action A").GridColumnCssClass("actions-sep").Icon(FA.Edit)
                .OnClick(x => x.Go<Admin.Settings.Administrators.EnterPage>().Send("item", "item.ID"));

ButtonColumn("Action B").HeaderText("Action B").GridColumnCssClass("actions-sep").Icon(FA.Edit)
    .OnClick(x => x.Go<Admin.Settings.Administrators.EnterPage>().Send("item", "item.ID"));


ButtonColumn("Action 1").HeaderText("Action").GridColumnCssClass("actions").Icon(FA.Edit)
    .OnClick(x => x.Go<Admin.Settings.Administrators.EnterPage>().Send("item", "item.ID"));


ButtonColumn("Action 2").HeaderText("Action").GridColumnCssClass("actions").Icon(FA.Edit)
    .OnClick(x => x.Go<Admin.Settings.Administrators.EnterPage>().Send("item", "item.ID"));


ButtonColumn("Action 3").HeaderText("Action").GridColumnCssClass("actions").Icon(FA.Edit)
    .OnClick(x => x.Go<Admin.Settings.Administrators.EnterPage>().Send("item", "item.ID"));
```
As you can see, we have set a custom title for the two `ButtonColumn()` and passed arbitrary `actions-sep` CSS class as a parameter to the `GridColumnCssClass()` method and for other action buttons we have passed `actions`.