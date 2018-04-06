# ConnectionString and config

In this tutorial we will see how to specify the connection string and how to get data from the config file. Like all ASP.Net Core projects, M# uses the standard **appsettings.json** file for storing the connection string of your project. This file also allows you to specify your custom application settings.

## Connection String

The Connection string specifies information about a data source and the means of connecting to it. It is stored in the **appsettings.json** file of your project as follows:

```JSON
"ConnectionStrings": {
        "AppDatabase": "Database=HelloWorld.AdHocTest; Data Source=localhost;Integrated Security=SSPI;MultipleActiveResultSets=True;"
    }
```

In the example above our *HelloWorld* project is a project using a TDD database mode, which means we have three different databases in our project and the current one is `HelloWorld.AdHocTest`.

> For more information about Database mode please refer to [Episode 1: Your First App](https://github.com/Geeksltd/MSharp.Docs/blob/master/Tutorials/1/README.md).


## Config

The `Config` class allows you to get data from the **appsettings.json** file. In this file you can put static data that will never change, like the key of a third party library, the URL of a payment gateway, ect. The method `Get()` helps you to access this data and has four overloads:

```C#
namespace Olive
{
    //
    // Summary:
    //     Provides shortcut access to the value specified in web.config (or App.config)
    //     under AppSettings or ConnectionStrings.
    public static class Config
    {
        //
        // Summary:
        //     Attempts to bind the given object instance to configuration values by matching
        //     property names against configuration keys recursively.
        //
        // Parameters:
        //   key:
        //     The key of the configuration section.
        //
        //   instance:
        //     The object to bind.
        public static void Bind(string key, object instance);
        //
        // Summary:
        //     Attempts to bind a new instance of given type to configuration values by matching
        //     property names against configuration keys recursively.
        //
        // Parameters:
        //   key:
        //     The key of the configuration section.
        //
        // Returns:
        //     A new instance of the given generic type.
        public static T Bind<T>(string key) where T : new();
        //
        // Summary:
        //     Gets the value configured in appSettings.json.
        public static string Get(string key);
        //
        // Summary:
        //     Gets the value configured in Web.Config (or App.config) under AppSettings. If
        //     no value is found there, it will return the specified default value.
        public static string Get(string key, string defaultValue);
        //
        // Summary:
        //     Reads the value configured in Web.Config (or App.config) under AppSettings. It
        //     will then convert it into the specified type.
        public static T Get<T>(string key);
        //
        // Summary:
        //     Reads the value configured in Web.Config (or App.config) under AppSettings. It
        //     will then convert it into the specified type. If no value is found there, it
        //     will return the specified default value.
        public static T Get<T>(string key, T defaultValue);
        //
        // Summary:
        //     Gets the connection string with the specified key.
        //     The connection strings should store directly under the ConnectionStrings section.
        public static string GetConnectionString(string key);
        //
        // Summary:
        //     Gets all the connection strings.
        //     The connection strings should store directly under the ConnectionStrings section.
        public static IEnumerable<KeyValuePair<string, string>> GetConnectionStrings();
        public static string GetOrThrow(string key);
        public static IConfigurationSection GetSection(string key);
        public static IConfigurationSection GetSectionOrThrow(string key);
        //
        // Summary:
        //     Determines whether the specified key is defined in configuration file.
        public static bool IsDefined(string key);
        //
        // Summary:
        //     Reads the app settings from a specified configuration file.
        [AsyncStateMachine(typeof(<ReadAppSettingsAsync>d__17))]
        [DebuggerStepThrough]
        [Obsolete("The XML settings are outdated.")]
        public static Task<Dictionary<string, string>> ReadAppSettingsAsync(FileInfo configFile);
        //
        // Summary:
        //     Gets the child nodes under a specified parent key.
        public static IEnumerable<KeyValuePair<string, string>> SettingsUnder(string key);
        //
        // Summary:
        //     Reads the value configured in Web.Config (or App.config) under AppSettings. It
        //     will then try to convert it into the specified type. If no vale is found in AppSettings
        //     or the conversion fails, then it will return null, or the default value of the
        //     specified type T.
        public static T TryGet<T>(string key);
    }
}
```

Here is an example of how to use those overloads:

```C#
public static void Analytics()
{
    // Get if analytics are enabled, if no value set false as default
    var activateAnalytics = Config.Get<bool>("Analytics:Enabled", defaultValue: false);

    // Get Analytics key
    var key = Config.Get<string>("Analytics:key");

    // Actions ...
}
```
