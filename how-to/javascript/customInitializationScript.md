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
public class SomePage : RootPage
{
    public SomePage()
    {
        JavaScript(JavascriptModule.Absolute("scripts/myScript.js"), "run()");
        //...
    }
}
```