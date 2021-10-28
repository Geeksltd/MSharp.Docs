# Adding a JavaScript library

## Problem

Sometimes your modules may need some 3rd-party libraries or dependencies. You should generally look for libraries that are active, have a good performance and supportive community and well documented.

 You want to know what steps you should follow to add JavaScript libraries.

## Implementation

 For this purpose, you should first add all needed libraries in the npm configuration file in `package.json`. You can add them in the `dependencies` section of this file.
```json
{
    //...
    "dependencies": {
        //...
        "chart.js": "^2.9.3",
    }
}
```

By doing this, Visual Studio will automatically download the packages. After adding libraries, then you can use this code:

```csharp
public class SomePage : RootPage
{
    public SomePage()
    {
        OnBound("JS dependency")
            .Code("var module = JavascriptModule.Absolute(\"scripts/myScript.js\")" +
                ".Add(JavascriptDependency.Absolute(\"lib/chart/dist/chart.js\"));" +
                "JavaScript(module);");
        //...
    }
}
```
M# will generate this code in the controller:
```csharp
[NonAction, OnBound]
public async Task OnBound(vm.EventSourcesList info)
{
    // JS dependency
    var module = JavascriptModule.Absolute("scripts/myScript.js")
        .Add(JavascriptDependency.Absolute("lib/chart/dist/chart.js")); 
	
    JavaScript(module);
    //...
}
```
Here **MvcJs** will first load and inject JS dependency named `chart.js` and then run the module named `myScript.js`. 

You can alternatively add the JS dependency to `references.js` instead of adding the dependency in the code. It then have a chance to get optimised, bundled, etc. This file is used to configure RequireJs and start-up libraries. You can find more info in the RequireJs [documentation](https://requirejs.org/docs/api.html#config).