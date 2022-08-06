# Sub Page's Functions / Methods

| Function Name|Description | Samples |
|--------------|-------------|--------|
Add||
AllowOutputCache|</br>If set to True, page level caching will be enabled using @OutputChahce page directive<br/><br/>WHEN TO USE/SET IT?<br/>When you want to cache the output of the page|
BaseController|<br/>Each page code behind class inherits MSharp.Framework.UI.Page class. Specifying any class name in this attribute will replace the base class of the code behind class of this page.<br/><br/> WHEN TO USE/SET IT?<br/>When you want to inherit a custom base class for the code behind class.|
BrowserTitle|<br/>In this field you can specify a browser title for the page. The resulting text will be rendered in the output HTML page in tag under area.<br/><br/>WHEN TO USE/SET IT?<br/>important to set it to a SEO friendly value if this page is a public facing page and search engines need to index it.
CommentTag|<br/>Any tag specified here will be shown before the page name in user interface section<br/><br/>WHEN TO USE/SET IT?<br/>When you want to tag a page for readability and ease of maintenance|
ControllerAttributes|<br/>Any attribute specified here will be generated in the @page directive.<br/><br/>WHEN TO USE/SET IT?<br/>Use this attribute to specify any attribute not available in M#|
ControllerCustomCode|<br/>This field act as a Quick class code. The code specified in this attribute will be generated just after the code-behind class definition.<br/><br/>WHEN TO USE/SET IT?<br/>When start up section doesn't fulfil the requirement and you want to write page level custom code.|
EnableSSL|<br/>If set to True, the page will be served only on https protocol If set to false, page is served on Http protocol only.<br/><br/>WHEN TO USE/SET IT?<br/>When you want to setup a page explicitly for secure or unsecure web protocol|
ExcludeFromChildrenUrl||
GetCurrent||
IsMultiLingual||
IsSPA||
Layout|<br/>In this field you can specify the template of the page.<br/><br/>Note:<br/>Be careful in selecting this template because your page totally is related to this template in visualization.<br/><br/>WHEN TO USE/SET IT?<br/>This field is mandatory and is set at the time of creating a page.|
LoadJavascriptModule||
LoadJavascriptService||
MarkupTemplate|<br/>Specify Html markup that will be used to layout the page. Use [#1#] as the placeholder for the first module on the page. or [#2#],... for the other modules.<br/><br/>WHEN TO USE/SET IT?<br/>When you want to layout a page and customize the arrangement of the modules registered on this page|
Name|<br/>Sets the name of this page. The ASPX page will be generated based on this name. Remember that it will be visible to the user in the browser address bar. Use a descriptive clear and short name.<br/><br/>Notes:<br/>M# will automatically replace space with hyphen.<br/>Do not use Pascal or Camel casing. Use separate clear words in plain English.<br/>A page&#39;s name together with its full hierarchy (name of its parent page, grand parent, etc) should characterise the page.<br/><br/>WHEN TO USE/SET IT?<br/>Every page must have a name.|
Roles|<br/>Use this attribute to select role(s) allowed to access this page.<br/><br/>Note:<br/>The page will only be accessible to the user of specified roles<br/><br/>WHEN TO USE/SET IT?<br/>When you need to enforce role based security.|
RootCssClass|<br/>In this field you can specify a css class of the page. Specifying a css class will generate a container element "span" with the given class and all the registered modules will be placed inside this container element.<br/><br/>Tips:<br/>css classes should always be lower case.<br/>Use "-" to separate the words in the css class.<br/>Use " " to separate multiple css classes.<br/><br/>WHEN TO USE/SET IT?<br/>When you need to apply any page specific design or layout related css|
Route||
RouteRoot||
RouteRootAnd|<br/>Makes this page respond to http requests to the application root url, i.e: / as well as other specified routes.|
Routes||
Set||
StyleDefinitions|<br/>In this field you can define inline css classes and rules. All css classes defined here are generated on the page inside tag<br/><br/>Note:<br/>Always define css styles and rules in css files and try to avoid inline css style definitions<br/><br/>WHEN TO USE/SET IT?<br/>In a very specific case when you need to use inline css styles|
UrlSegment|<br/>Normally the children of this page get the name of this page as part of their url.<br/>If you want to remove this from its children's urls, then set UrlSegment to [#EMPTY#]. Or if you want it to be shorter than its name, then provide a brief value.<br/><br/>WHEN TO USE/SET IT?<br/>For example if your deep page has the value of /administrator/cms/products/view/{id} you can use UrlSegment on the parent pages to turn it into: /admin/products/{id}|
ValidateRequest|<br/>If this field is set to False the system stops to validate incoming requests.<br/><br/>Note:<br/>Setting this to False could make it vulnerable to Cross Site Scripting<br/><br/>WHEN TO USE/SET IT?<br/>This is done in pages which you want to allow user enter HTML contents.|

# Sub Page's Events/CallBack

| Event Name|Description | Samples |
|--------------|-------------|--------|
OnStart||