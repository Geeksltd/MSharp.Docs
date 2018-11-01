# Merging Columns

By default **M#** generate each action button to a seperate table cell. For instance, here you can see we have 5 action buttons that consume large space:

![1](https://user-images.githubusercontent.com/1321544/46538501-16b4ef80-c8c1-11e8-8570-3c2ea3991f59.PNG)

As you can see we have lost lots of spaces for these buttons, to make base use of space you can merge buttons in a single drop-down list. For this purpose, you should open `package.json` and update `olive.mvc` package to the latest version.
After updating `olive.mvc` package, all action buttons which have `.actions-merge` CSS class would be merged into a single cell.

![2](https://user-images.githubusercontent.com/1321544/46538813-cdb16b00-c8c1-11e8-9f07-a1cf75289079.PNG)

![3](https://user-images.githubusercontent.com/1321544/46538827-d99d2d00-c8c1-11e8-83e3-bc95a0862ca5.PNG)

In the more complex scenario, you may need to just merge some of the action buttons and not all of them. As you can see in this picture, we need to have two separate action buttons and other actions should be merged:

![4](https://user-images.githubusercontent.com/40687782/46793408-8ef63780-cd3d-11e8-977b-39ae786a54dc.png)

To generate this, you just need to set same title for your prefered `ButtonColumn` and add `actions-merge` CSS class:

```csharp
 ButtonColumn("Action A").HeaderText("Action A").GridColumnCssClass("actions").Icon(FA.Edit)
                .OnClick(x => x.Go<Admin.Settings.Administrators.EnterPage>().Send("item", "item.ID"));

ButtonColumn("Action B").HeaderText("Action B").GridColumnCssClass("actions").Icon(FA.Edit)
    .OnClick(x => x.Go<Admin.Settings.Administrators.EnterPage>().Send("item", "item.ID"));


ButtonColumn("Action 1").HeaderText("Action").GridColumnCssClass("actions-merge").Icon(FA.Edit)
    .OnClick(x => x.Go<Admin.Settings.Administrators.EnterPage>().Send("item", "item.ID"));


ButtonColumn("Action 2").HeaderText("Action").GridColumnCssClass("actions-merge").Icon(FA.Edit)
    .OnClick(x => x.Go<Admin.Settings.Administrators.EnterPage>().Send("item", "item.ID"));


ButtonColumn("Action 3").HeaderText("Action").GridColumnCssClass("actions-merge").Icon(FA.Edit)
    .OnClick(x => x.Go<Admin.Settings.Administrators.EnterPage>().Send("item", "item.ID"));
```