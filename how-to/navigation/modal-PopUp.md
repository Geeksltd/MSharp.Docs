# Modal (Pop-up)

## Problem

You want a page to open as a Pop-up instead of redirecting the user. Modal pages are especially useful for creating new items, where the user will want to go back to the original page when the process is completed.

## Implementation

1) Give the page a Modal Layout – Msharp features a predesigned layout AdminDefaultModal

```csharp

    public class EnterPage : SubPage<ContactsPage>
    {
        public EnterPage()
        {
            Layout(Layouts.AdminDefaultModal);
            Add<Modules.ContactForm>();
        }
    }

```

2) When navigating to the page, open it as a Popup() instead of using Go()

```csharp

        public ContactsList()
        {
            HeaderText("Contacts");
            
            Column(x => x.Name);
            Column(x => x.Phone);
            
            ButtonColumn("Edit").HeaderText("Actions").GridColumnCssClass("actions").Icon(FA.Edit)
                .OnClick(x=> x.PopUp<Contact.EnterPage>().Send("item", "item.ID"));
                
            Button("New Contact").Icon(FA.Plus)
                .OnClick(x => x.PopUp<Contact.EnterPage>());
        }
```

3) When Navigating away from the pop up, make sure the Modal is closed instead of being redirected

```csharp

        public ContactForm()
        {
            HeaderText("Contact details");
            
            Field(x => x.Name).Control(ControlType.Textbox);
            Field(x => x.Phone).Control(ControlType.Textbox);
            
            Button("Cancel")
                .CausesValidation(false)
                .OnClick(x => x.CloseModal());
            
            Button("Save").IsDefault().Icon(FA.Check)
            .OnClick(x =>
            {
                x.SaveInDatabase();
                x.GentleMessage("Saved successfully.");
                x.CloseModal(Refresh.Ajax);
            });
        }

```

Adding Refresh.Ajax to CloseModal() means the parent page is reloaded when the modal page is closed.
