# Custom initialization script

## Problem

Sometimes you need to create custom javascript modules that are loaded for specific pages as opposed to the whole application.

## Implementation

For example if your script file is under wwwroot/scripts/components/myScript.js you can load it by running the following Javascript code:

```javascript
window.loadModule('/scripts/components/myScript');
```

Or if you want to run a static function of your module named *Run* as soon as it's loaded, you can use:

```javascript
window.loadModule('/scripts/components/myScript', m => m.default.Run());
```
To achieve this in M#, instead of writing the code shown above, in the Page definition file where you want this script to be loaded, simply call the *JavaScript()* method as shown below:
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
M# will generate this code:
```csharp
[NonAction, OnBound]
public async Task OnBound(vm.EventSourcesList info)
{
    // Load module
    JavaScript(JavascriptModule.Relative("scripts/myScript.js"), "run()");
    //...    
}
```
*JavascriptModule* has two important static methods, `Absolute` and `Relative`. If you are developing a micro-service and it has a JS file in its scripts folder, then you must use `Absolute` method to load this file from current micro-service, but if you want to load a JS file from *Hub* project, then you must use `Relative` method. Here we have used `Absolute` path as you see below:

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
Using this method, JavaScript code is registered on the server-side. Then on the client-side, it will get added as a task to a hidden field named `Startup.Actions` along with other M# generated tasks and form an array of Javascript instructions as a JSON array. 
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