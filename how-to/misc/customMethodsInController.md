# Custom methods in the controller

## Problem

You need to add a method in the controller class. You can't add it directly because it gets replaced by the M# compiler's generated code.

### Usage
You may have multiple code statements that run on an event handler and can't be factored out to the domain logic because it may involve operations on the ViewModel class. In this case, you may put the code for the presentation logic in a separate method in the controller and call it from the handler. 

Another usage maybe when you have a block of code that should be run in more than one place in the controller.

## Implementation

You can add your methods using `OnControllerClassCode` method in M# module classes.

``` csharp
// In UI Module class
OnControllerClassCode("Get clients")
    .Code(@"
        async Task<IEnumerable<Client>> GetClients(vm.CountryGroupsForm info)
        {
            return await info.Country.Clients;
        }
    ");
```
M# will generate the following code in the generated controller class:
``` csharp
//Get clients
async Task<IEnumerable<Client>> GetClients(vm.CountryGroupsForm info)
{
    return await info.Country.Clients;
}
```

This code is placed in a partial class for the controller for being separate from the action methods.
