# How to use hierarchy

## Problem

Sometimes you need to create a parent/child pattern in your application which parent and all children have the same type and they should be displayed in a hierarchy order. To achieve this, you should create a property with the same type of the class which is usually called **Parent** and a collection of the children, then you should add some validation to prevent any potential loop -in your application which could be time consuming but M# will help you through this in the easiest way.

## Implementation
Because hierarchy is a very repetitive scenario, M# has a built-in feature to implement it in the easiest way. For instance, consider `Node` class as a parent that possess many children with the same type as their parent and we have a tree list of them. To achieve this M# provide `IsHirarchy()` method which will ease the creating of the parent/child pattern by providing some extra methods and validations.

### Example
Let's say we need a `Node` class which has many children and each child will have a parent, our ultimate goal is to have a tree list of nodes.

```csharp
using MSharp;

namespace Domain
{
    public class Node : EntityType
    {
        public Node()
        {
            IsHirarchy().ToStringExpression("this.GetFullPath()");

            String("Name").Mandatory();

            Associate<Node>("Parent");

            InverseAssociate<Node>("Children", "Parent");
        }
    }
}
```
As you can see above, we have used `IsHirarchy()` method here which will cause `Node.cs` class inherits from [IHierarchy](http://learn.msharp.co.uk/#/Domain/Advanced/MSharpInterface?id=hierarchy) interface. This special interface will add some extra validations and methods that will be very handy for hierarchy. Here is defination of some of them:

- `.GetAllChildren()`: Get all children hierarchy of the selected node.
- `.GetAllParents()`: Get all parent hierarchy of the selected node.
- `.GetParent()`: Get parent hierarchy of the selected node.
- `.GetFullPath()`: Get full path of the selected node.

Moreover, M# will add some extra validation which will prevent the client to create a loop in the hierarchy accidentally, which is very susceptible when there are lots of parents available.