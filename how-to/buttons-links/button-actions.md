# Button actions

Every button on M# has a Workflow, which contains a collection of Actions which are stated via the OnClick method of the button. Below is the list of most common actions which are mostly self explanatory:

+ Configuration:
    + RunInTransaction: By default all actions are executed in a single transaction scope. We can change this behaviour by calling RunInTransaction and passing a false argument to it. For more info please review the [Transaction section](how-to/buttons-links/transactions.md).
+ Database:
    + SaveInDatabase: we can use this action usually on create or update form buttons.
	+ DeleteItem: We can use this action on list modules.
+ Window or Browser Behaviour:
    + CloseBrowserWindow
    + CloseModal
+ Navigation:
	+ BrowserBack
	+ Go
	+ ReturnView
	+ ReturnToPreviousPage
	+ RefreshPage
	+ PopUp
+ Messaging:
	+ MessageBox
	+ GentleMessage
	+ ShowPleaseWait
	+ Display
+ Export/Print:
	+ PrintPage
	+ Export (cvs,excel,EpPlus)
+ Javascript:
	+ Javascript
	+ LoadJavascriptModule
    + LoadJavascriptService

In order to create execution branches based on condition we can chain each of the actions with conditional methods of the fluent API like If ElseIf Else M# provides common conditions as an enum named CommonCriterion. You can define your own Rules on the logic of each Entity.

If we need to execute a method which we wrote for our entities on the Domain project > Logic we can call them by using CSharp Action.

```csharp
using MSharp;

namespace Modules
{
    public class RegistrationForm : FormModule<Domain.Registration>
    {
        public RegistrationForm()
        {
            HeaderText("Register for Event");

            Field(x => x.FirstName).Mandatory();

            Field(x => x.LastName).Mandatory();

            Field(x => x.Email).Mandatory();

            Field(x => x.IsSubscribed)
                .Label("Interested in our Newsletter?")
                .TrueText("Yes, I'd like to subscribe and receive your newsletter")
                .FalseText("No, thanks.");

            Button("Cancel").OnClick(x => x.ReturnToPreviousPage());

            Button("Save").IsDefault().Icon(FA.Check)
            .OnClick(x =>
            {
                x.RunInTransaction(false);
                x.SaveInDatabase();
                // SendConfirmation is part of the Registration Entity's logic
                x.CSharp("info.Item.SendConfirmation();"); 
                x.Display("Saved successfully.")
                .DisplayOnModule();
            });
        }
    }
}

```