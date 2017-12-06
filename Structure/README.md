# Structure of an M# solution
When you create a new M# ASP.NET project you will see the following structure in Visual Studio.

![](Solution.JPG)

## @Model
This is where you define your application entities.
An entity represents a real world object which exists in a business domain. In M# development you always start here. Think of it as your database design stage, but at a more conceptual level. Here you declare your business data types and their associations, which will be the foundation of everything else.

>- This project does not reference any other project in your solution.
>- It references the core [M# nuget package](https://www.nuget.org/packages/MSharp/)
>- The compiled output of this prject will not be deployed and will not be used at runtime by your application.
>- It's only used during development.

## Domain
This is the home for your business domain objects and business logic. By default you will have the following folders In this project you will have:
>-
This M# intelligently converts an Entity Domain Model, with all the associations and relationships, into database tables while maintaining entity relationships. This eliminates the need of developing Database and Business entities separately, significantly reducing the development time.

M# fully supports Object Oriented development and encourages developers to use all such features exposed at entity and property level.
