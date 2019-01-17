# Migrating from Json (web-based IDE) to MC# (Visual Studio based)

......

# Migrating apps from .NET Framework to .NET Core

1. First convert the application to MC#
1. Create a new M# .NET Core app
1. Copy these files from the converted MC# app to the newly generated .NET Core app:
   - M#\Model\*.*
   - M#\UI\*.*

## Renamed namespaces, types & methods
The following elements are renamed in the framework. In your application, you should change all references to the old names.
- MSharp.Framework → Olive
- Database.Find() → Database.FirstOrDefualt()
- Document → Blob
- IEmailQueueItem → IEmailMessage 
- IApplicationEvent → IAuditEvent 
- IHttpActionResult → IActionResult or Task<IActionResult>
- RoutePrefix(Attribute) → Route(Attribute).
- [Authorized] → [JwtAuthenticate]

## Tips:
- Most extension methods which were defined in the System (namespace) before. Now they are in Olive. When you face missing methods, check the suggested using-list.
- Many methods are changed to async. When your method calls them, your method should also become async. This is recursive all the way up.
- If you use email sending:
  - If your new app is a monolithm add a NuGet reference to Olive.Email package
  - If your new app is a Microservice, just reference the EmailApi nuget package and use that, similar to other microservices.
- If your new app is a Microservice, remove `ApplicationEvent` entity. Logging is handled centrally in Microservices (in Audit service).
- Instead of using User in the controllers and views to reference the current user use GetUser() method.
