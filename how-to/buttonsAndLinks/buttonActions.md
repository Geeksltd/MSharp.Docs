# Button actions

## Problem

When you have a button on a module, you almost definitely want it to do something once clicked.

## Implementation

M# has the `Onclick(x => x.[Method])` method where we can define what should happen when a button is clicked.  There are many actions that can be created.  Here are some of the most useful actions.

### Examples

#### `Go<>()`

This is a useful action to allow you to use buttons (but primarily links) to navigate to other pages in the application

```csharp
namespace Modules
{
    class AdminCMSPrivacyPolicyView : ViewModule<Domain.CMSPrivacyPolicy>
    {
        public AdminCMSPrivacyPolicyView()
        {
            DataSource("await Database.Of<CMSPrivacyPolicy>().FirstOrDefault()");
            HeaderText("Privacy Policy");
            IsViewComponent();

            Field(x => x.Body);
            Markup(@"<div>@Html.Raw(item.Body)</div>");
            Button("Edit")
               .OnClick(x => x.Go<Admin.CMS.PrivacyPolicy.EnterPage>().Send("item", "item.ID"));
        }
    }
}
```

In this example, you can also see the use of `Send()` where we can pass an item to use as a `RequestParam()` in the new page.

#### `SaveInDatabase()`

This is the default save feature in M# that creates this code in the controller. 

```CSharp
public async Task<bool> SaveInDatabase(vm.ApplicantOwnSolicitorForm info)
        {
            if (!ModelState.IsValid(info))
            {
                Notify(ModelState.GetErrors().ToLinesString(), "error");
                return false;
            }

            var item = info.Item.IsNew ? info.Item : info.Item.Clone();

            await info.CopyDataTo(item); // Read the ViewModel data into the domain object.

            using (var scope = Database.CreateTransactionScope())
            {
                try
                {
                    info.Item = await Database.Save(item);

                    scope.Complete();
                    return true;
                }
                catch (Olive.Entities.ValidationException ex)
                {
                    Notify(ex.ToFullMessage(), "error");
                }

                return false;
            }
        }
```

 This saves the data populated in a form to the database.

#### `CloseModal()`

If your module is going to live on a pop up, then adding this method to the `OnClick()` method will close the pop up and return the user to the parent page.

#### `If()`, `Else()` and `CSharp()`

These 3 tend to be used in conjunction with each other quite frequently

```CSharp
 Button("Save").IsDefault().Icon(FA.Check)
    .OnClick(x =>
    {
        x.CSharp("var isNew = info.Item.IsNew;");
        x.SaveInDatabase();
        x.If("isNew").CSharp(@"
                await MortgageSolicitorService.ActivateSolicit(info.Item.Application, info.Item);
                await new MortgageApplicationServi(info.Item.Application).MarkSolicitorDetailsAsComplete;");
        x.UpdateMortgageApplicationStatus("info.Item.Application");
        x.GentleMessage("Saved successfully.");
        x.If(AppRole.Advise.Go<Adviser.ViewApplication.Solicitor.SolicitorPage>().Se("application", "info.Item.Application.ID");
        x.If(AppRole.Admin).Go<Admin.Applicants.SolicitorPage>().Se("application", "info.Item.Application.ID");
        x.Else().Go<Applicant.SolicitorInformationPage>();
    });
```

The `If()` and `Else()` methods work like if and else statements in C#.  The `CSharp()` method allows us to write C# code directly into the controller.  The first `If()` and `CSharp()` instances create the following code in the controller.

```CSharp
if (isNew)
    {
        await MortgageSolicitorService.ActivateSolicitor(info.Item.Application, info.Item);
        await new MortgageApplicationService(info.Item.Application).MarkSolicitorDetailsAsComplete();
    }
```
