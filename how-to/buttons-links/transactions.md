# Transactions

Each button is associated with a series of workflows which are defined by chaining the button method with OnClick method. By default these workflows are executed in one transaction scope so in case of any runtime error all the previous steps can be rolled back. In some scenarios executing all the steps in the workflow is not desirable for example when we are registering a new user and we need to send an email to the user in order to confirm the user's email address. We need to send the confirmation email after successful storage of the user’s information and we don’t want the record deletion in case of email dispatch failure, therefore we must instruct M# to execute each of the workflow’s steps on different scope, to do so we use `RunInTransaction(false)` method. 

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
                    x.CSharp("await info.Item.SendConfirmation();");
                    x.Display("Saved successfully.")
                        .DisplayOnModule();
                });
        }
    }
}
```

This example is part of the [M# Tutorial - Episode 14: Sending email ](/Tutorials/14/README)