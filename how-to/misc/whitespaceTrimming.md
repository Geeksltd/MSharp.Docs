# white-space trimming

## Problem

Sometimes, if not careful, users might enter additional white-space in their input or the data you read from some other API gateway/database might contain additional white-space due to specific formats or human errors.

However, sometimes you actually might want the white-space at the beginning or end of the string.

M# allows you to choose what to do with the white-space at the beginning or end of the string.

## Implementation

By default, M# trims all string values.
You can turn this off if you need to by using the `TrimValues()` method.
It takes a bool which indicates if the value should be trimmed.
The default value of it is true and you only need to call it on a property if you want to turn trimming off.

#### Example

Let's say we have an entity of texts of a poster that needs to be exactly used for creating the final image and sometimes string parts need additional spacing for formatting purposes. 
We define the entity like this


```csharp

using MSharp;

namespace Model
{
    public class PosterData : EntityType
    {
        public PosterData()
        {
            String("First").Mandatory().TrimValues(false);
            String("Second").Mandatory().TrimValues(false);
            String("Third").Mandatory().TrimValues(false);

            String("Author").Mandatory();
        }
    }
}
```

As you can see, we have 3 text values other than the poster's author name which should be inserted on the image. we disable trimming on them so if the artist wanted to put a space at the beginning of one of them, it is not trimmed and a correct result is produced.
