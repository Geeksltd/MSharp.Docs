# M# Concepts:
## Entity, Page, Module
This lesson gives a bird’s eye view of the core components of M#. The web application structure in M# heavily depends on components described below, which are discussed in further detail within individual chapters. A developer must understand these components in order to effectively develop and maintain quality web applications in M#.

### Entity
An entity represents a real world object, distinguishable from other entities, which exists in a business domain. In M# the same exact definition is undertaken. In M# the first thing a developer needs to do is to build a concrete business domain model, which consists of entities often referred to as business objects.

M# intelligently converts an Entity Domain Model, with all the associations and relationships, into database tables while maintaining entity relationships. This eliminates the need of developing Database and Business entities separately, significantly reducing the development time.

M# fully supports Object Oriented development and encourages developers to use all such features exposed at entity and property level.

## Adding New Entity
A new entity can be added by right click on your custom folder in **#Model** project and select **Add Entity** from M# context menu as shown bellow
!["M# Add Entity"](ConceptsImages/AddEntity.PNG "M# Add Entity")