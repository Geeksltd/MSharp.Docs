# Merging Columns

By default **M#** generate each action button to a seperate table cell. For instance, here you can see we have 5 action buttons that consume large space:

![1](https://user-images.githubusercontent.com/1321544/46538501-16b4ef80-c8c1-11e8-8570-3c2ea3991f59.PNG)

If you need to merge these action buttons to a one drop-down list button you should open `bower.json` and update `olive.mvc` package to the latest version.
After updating `olive.mvc` package all action buttons which have `.actions` CSS class would be merged into a single cell and their action title would be merged too.

![2](https://user-images.githubusercontent.com/1321544/46538813-cdb16b00-c8c1-11e8-9f07-a1cf75289079.PNG)

![3](https://user-images.githubusercontent.com/1321544/46538827-d99d2d00-c8c1-11e8-83e3-bc95a0862ca5.PNG)

Please bear in mind that if you don't want this behaviour for some part of your pages you can simply change default CSS class of your action button to something else like `ButtonColumn("New House").HeaderText("Actions1")`.