# Custom initialization script

## Problem
There are some cases where you need a Javascript file to be referenced on a specific page or module only or with a condition as opposed to the whole application. For example when you need to reference the Google Maps scripts.

## Implementation
Script loading can be done in both JavaScript and M#.

### In JavaScript
In JavaScript, you can load your script file by running the following code:

```javascript
window.loadModule('/scripts/components/myScript');
```
Here your script file is under _wwwroot/scripts/components/myScript.js_

Similarly, if you want to run a static function of your module named `Run` as soon as it's loaded, you can use:

```javascript
window.loadModule('/scripts/components/myScript', m => m.default.Run());
```

### In M#
To achieve this in M#, instead of writing the code shown above, in the Page definition file where you want this script to be loaded, simply call the `JavaScript` method as shown below:
```csharp
public class SomePage : RootPage
{
    public SomePage()
    {
        LoadJavascriptModule("scripts/myScript.js");
        //...
    }
}
```
M# will generate this code in the controller:
```csharp
[NonAction, OnBound]
public async Task OnBound(vm.EventSourcesList info)
{
    // Load module
    JavaScript(JavascriptModule.Relative("scripts/myScript.js"), "run()");
    //...    
}
```
`JavascriptModule` has two important static methods, `Absolute` and `Relative`. If you are developing a micro-service and it has a JS file in its scripts folder, then you must use `Absolute` method to load this file from current micro-service, but if you want to load a JS file from *Hub* project, then you must use `Relative` method. Here we have used `Absolute` path as you see below:

```csharp
public class SomePage : RootPage
{
    public SomePage()
    {
        LoadJavascriptModule("scripts/myScript.js", absoluteUrl: true);
        //...
    }
}
```

M# will generate this code:

```csharp
[NonAction, OnBound]
public async Task OnBound(vm.EventSourcesList info)
{
    JavaScript(JavascriptModule.Absolute("scripts/myScript.js"), "run()");
    //...
}
```

## Server-side vs client-side
By using this method in M#, JavaScript code is registered on the server-side. Then on the client-side, it will get added as a task to a hidden field named `Startup.Actions` along with other M# generated tasks and form an array of Javascript instructions as a JSON array. 
```html
<form data-module="ClientsList" method="get" action="@Url.Current()" data-redirect="ajax">
   @Html.StartupActionsJson()
    <!-- ... -->
</form>
```
In this code `StartupActionsJson` method is defined in Olive as follows:
```csharp
public static IHtmlContent StartupActionsJson(this IHtmlHelper @this)
{
    if (!@this.Request().IsAjaxPost()) return null;
    var startupActions = @this.GetActionsJson().ToString().Unless("[]");
    if (startupActions.HasValue())
    {
        @this.ClearActionsJson();
        return @this.Hidden("Startup.Actions", startupActions);
    }
    return HtmlString.Empty;
}
```

Those instructions are executed one by one in **olivePage.ts** in MvcJs library, which is inherited by **appPage.ts**.
```typescript
protected onViewChanged() 
{
    const standardAction = this.getService<StandardAction>(Services.StandardAction);
    standardAction.runStartup(container, trigger, "PreInit");
    //...
}
```

Each task can be scheduled for either `PreInit` or `Init` (default) stage. `PreInit` tasks run before the `initialize` method, and Init tasks after.

### Note
If you need a JavaScript file to be added to the entire website unconditionally, you should add it to the `references.js` file that is used to configure RequireJs. It's the best practice as it gets optimised, bundled, etc.