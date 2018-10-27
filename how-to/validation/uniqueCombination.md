# Unique Combination

## Problem

In many applications, having the ability to specify a single property as unique is not enough.
You need to specify a combination of properties to be unique.

In many cases that you have a relation, say books in a store or children in a family or students in a school, the students/children/books should have something unique only in their school/family/store.
This means a student ID doesn't have to be unique overall for a school system, it only has to be unique in the school.
For cases like these and many other places, the uniqueness value is a combined one where for example, student ID and school combination should be unique but neither school or student ID has to be unique in the system.

## Implementation

You should use the `UniqueCombination()` method in your entity definition code to specify a set of properties to be unique when combined (i.e. the set of values for all of them together, should be unique but each of them on its own, or any subset of it, doesn't have to be unique).

If you specify properties `A` and `B` as the unique combination of properties which should be unique, then values of `A` or `B` can be non-unique on their own.
Let's say each of them can have a value between 1 and 10.
You can have 5 entities which their `A`, has the value 5 but each of them has to have a different value of `B` combined with it.
You however cannot have two entities which both their `A` and `B` have the same value.

Let's clarify with an example:
If we display the combined value of `A` and `B` as a single number like the following example: First put the value of `A` and then `B`, so if `A` is 3 and `B` is 7, we display their value as 37.
Then the following facts are true

-  33, 34, 35 all are valid because despite having the same `A` , their `B` is different
- 34, 24, 14 are valid for different entities because despite having the same `B`, their `A` is different
- 24, 33, 24 are not a valid set of values for different entities because the set of entities will end up with two entities which have `A` equal to 2 and `B` equal to 4

The same is true for a combination of any number of properties.

The `UniqueCombination()` method takes an array of strings which are the names of the properties which their combination should be unique.
Let's follow with an example.

#### Example

We have a system for schools to manage their students.
Each student ID should be unique in their own school so we should define the combination of student's ID and school to be unique.

The school entity is very simple for our example to not complicate matters

```csharp
using MSharp;

namespace Domain
{
    public class School :EntityType
    {
        public School()
        {
            String("Name").Mandatory();
        }
    }
}

```

Actual requirements of the `School` entity will be more complex but we don't want to deal with anything which is not needed for our example. 

Let's define the `Student` entity which is the main part of our example

```csharp
using MSharp;


namespace Domain
{
    public class Student : EntityType
    {
        public Student()
        {
            String("First Name").Mandatory();
            String("Last Name").Mandatory();
            Int("StudentID").Mandatory();
            Associate<School>("School").Mandatory();
            UniqueCombination(new string[] { "StudentID", "School" });
        }
    }
}

```

As you can see the student has a relation with the school which he/she studies in.
It also has an ID property called `StudentID` which their combination should be unique.
For this purpose we call `UniqueCombination()` with the `StudentID` and `School` properties.

#### Generated Code

The generated code for `School` doesn't have anything special so we will not list it here.
However the `Student` entity worth examining

```csharp
public partial class Student : GuidEntity
{
        CachedReference<School> cachedSchool = new CachedReference<School>();
        
        /// <summary>Gets or sets the value of StudentID on this Student instance.</summary>
        public int StudentID { get; set; }
        
        /// <summary>Gets or sets the ID of the associated School.</summary>
        public Guid? SchoolId { get; set; }
        
        /// <summary>Gets or sets the value of School on this Student instance.</summary>
        public School School
        {
            get => cachedSchool.Get(SchoolId);
            set => SchoolId = value?.ID;
        }
        
        /// <summary>
        /// Find and returns an instance of Student from the database by its School and StudentID.<para/>
        /// If no matching Student is found, it returns Null.<para/>
        /// </summary>
        /// <param name="school">The School of the requested Student.</param>
        /// <param name="studentID">The StudentID of the requested Student.</param>
        /// <returns>The matching Student instance or otherwise null.</returns>
        public static Task<Student> FindBySchoolAndStudentID(Domain.School school, int studentID)
        {
            return Database.FirstOrDefault<Student>(s => s.SchoolId == school && s.StudentID == studentID);
        }
        
        /// <summary>
        /// Validates the data for the properties of this Student and throws a ValidationException if an error is detected.<para/>
        /// </summary>
        protected override async Task ValidateProperties()
        {
            var result = new List<string>();
            
            if (FirstName.IsEmpty())
                result.Add("First Name cannot be empty.");
            
            if (FirstName?.Length > 200)
                result.Add("The provided First Name is too long. A maximum of 200 characters is acceptable.");
            
            if (LastName.IsEmpty())
                result.Add("Last Name cannot be empty.");
            
            if (LastName?.Length > 200)
                result.Add("The provided Last Name is too long. A maximum of 200 characters is acceptable.");
            
            if (SchoolId == null)
                result.Add("Please provide a value for School.");
            
            if (StudentID < 0)
                result.Add("The value of StudentID must be 0 or more.");
            
            // Ensure uniqueness of School and StudentID
            // Find an existing Student with the same School and StudentID
            
            if (await Database.Any<Student>(s => s != this && s.StudentID == StudentID && s.SchoolId == SchoolId))
            {
                throw new ValidationException("There is an existing Student with the same School and StudentID in the database already.");
            }
            
            if (result.Any())
                throw new ValidationException(result.ToLinesString());
        }
}
```

As you can see in `ValidateProperties()` there is a section which checks if the combination of `StudentID` and `School` is unique

```csharp            // Ensure uniqueness of School and StudentID
            // Find an existing Student with the same School and StudentID
            
            if (await Database.Any<Student>(s => s != this && s.StudentID == StudentID && s.SchoolId == SchoolId))
            {
                throw new ValidationException("There is an existing Student with the same School and StudentID in the database already.");
            }
```

Other than this, we have a method called `FindBySchoolAndStudentID()` which helps us to find a student by supplying the student ID and school of the student.

## Remarks

- The generated `FindByXXX()` method allows searching by all of the properties combined since this is the only way to make sure, the exact unique entity will be returned.
XXX here is the name of the properties which we are searching with.
- In our example, probably the `Student` 's primary key should have been set to its `StudentID` by calling `IsPrimaryKey()` on it and calling `PrimaryKeyType("int")` in the entity definition but it wasn't related to the example so we did not complicate it by doing these things.
_ also the `School` entity should have a unique name and lots of other properties and maybe a special type of `SchoolID` based on the country regulations but they were not relevant to our example either