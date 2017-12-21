# M# Shortkeys and Editing Tips
A set of tips to make your more productive.

## Intellisense for custom code fragments
In M# in many places you can add C# code in the middle of your M# definitions. For example to specify the default value for a property.

Let's say you have the following definition:
```csharp
public class SomeType: EntityType
{
        public SomeType()
        {
            ...
            DateTime("Date").Mandatory().Default("C#:LocalTime.Now");
        }
}
```
In the above example, the default value expression is a **constant string**, which ultimately will be generated in the target Domain entity code. So you know that its true *nature* is a ***C# expression***, while in the M# definition file, it's just plain string. It would be often handy to use intellisense for code completion and checking write at this level to ensure your code fragment is valid.


1. Put the cursor anywhere on the text, i.e. "C#:LocalTime.Now".
2. Press Alt + i
3. A small pop-up window will appear, giving the context of the target code, enabling full intellisense.
4. Write the code and press Ctrl + S.
5. The pop-up will automatically hide.
6. In the above example, the new code will appear as the argument of Default() method.
