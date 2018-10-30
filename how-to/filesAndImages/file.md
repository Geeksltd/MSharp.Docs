# Handling files and documents

## problem

Some entities need to store files with them. 
Users of a job/talent seeking website need to store their resumes for potential employers with them.
Engineering related sites might need to special software files with the results in the system for reproduction/observation purposes.

Files should be uploadable using entity creation/modification forms.
M# allows us to do all of these in an easy to use manner.

## Implementation

The `SecureFile()` property can be used in an entity so the form using it will allow the user to upload a file.
The file will be stored on the disk in a configurable folder and the address of the file will be stored in the database table.
You can allow specific file extensions when validating your forms.


#### Example

Let's say we have an application to store tests results of a lab.
Each test result contains a name, a date and a description.
It also contains a `CSV` file which contains the exact test results which can be used to view them in excel or another program.
We define the entity like this

```csharp
using MSharp;

namespace Domain
{
    public class TestResult : EntityType
    {
        public TestResult()
        {
            String("Name").Mandatory();
            Date("Date").Mandatory();
            String("Description").Mandatory();
            SecureFile("Data").Mandatory();
        }
    }
}
```

The `Data` property is a file which is stored in the entity.
We can limit the extension of the file easily using the `ValidExtensionss()` method but we don't want to complicate the example for now.
This entity's form will allow the user to upload a file while entering other fields of the form as well.

#### Generated Code

The generated class looks like this

```csharp
public partial class TestResult : GuidEntity
{
        /// <summary>Stores the binary information for Data property.</summary>
        private Blob data;
        
        /// <summary>
        /// Gets or sets the value of Data on this Test result instance.<para/>
        /// When a download request comes, the system will call my method IsDataVisibleTo(IUser) which must return True for only permitted users.<para/>
        /// </summary>
        [Newtonsoft.Json.JsonIgnore]
        [SecureFile]
        public Blob Data
        {
            get
            {
                if (data is null) data = Blob.Empty().Attach(this, "Data");
                return data;
            }
            
            set
            {
                if (!(data is null))
                {
                    // Detach the previous file, so it doesn't get updated or deleted with this Test result instance.
                    data.Detach();
                }
                
                if (value is null)
                {
                    value = Blob.Empty();
                }
                
                data = value.Attach(this, "Data");
            }
        }
        
        /// <summary>Gets or sets the value of Date on this Test result instance.</summary>
        [DateOnly]
        public DateTime Date { get; set; }
        
        /// <summary>Gets or sets the value of Description on this Test result instance.</summary>
        public string Description { get; set; }
        
        /// <summary>Gets or sets the value of Name on this Test result instance.</summary>
        public string Name { get; set; }
        
        /// <summary>Returns a clone of this Test result.</summary>
        /// <returns>
        /// A new Test result object with the same ID of this instance and identical property values.<para/>
        ///  The difference is that this instance will be unlocked, and thus can be used for updating in database.<para/>
        /// </returns>
        public new TestResult Clone()
        {
            var result = (TestResult) base.Clone();
            
            result.Data = Data.Clone();
            return result;
        }
        
        /// <summary>
        /// Validates the data for the properties of this Test result and throws a ValidationException if an error is detected.<para/>
        /// </summary>
        protected override Task ValidateProperties()
        {
            var result = new List<string>();
            
            if (Data.IsEmpty())
            {
                result.Add("It is necessary to upload Data.");
            }
            
            // Ensure the file uploaded for Data is safe:
            
            if (Data.HasUnsafeExtension())result.Add("The file uploaded for Data is unsafe because of the file extension: {0}".FormatWith(Data.FileExtension));
            
            if (Description.IsEmpty())
                result.Add("Description cannot be empty.");
            
            if (Description?.Length > 200)
                result.Add("The provided Description is too long. A maximum of 200 characters is acceptable.");
            
            if (Name.IsEmpty())
                result.Add("Name cannot be empty.");
            
            if (Name?.Length > 200)
                result.Add("The provided Name is too long. A maximum of 200 characters is acceptable.");
            
            if (result.Any())
                throw new ValidationException(result.ToLinesString());
            
            return Task.CompletedTask;
        }
}
```

There are multiple things to note:

- `Blob` is an M# type to represent binary data (blob stands for binary large object)
- The file uses a backing field and the property unlike other properties which don't have any backing fields
- `ValidateProperties()` checks to see if the file has any unsafe extensions. That's for security reasons to not allow the user to upload files which can compromise the server.
- The `Clone()` method clones the file separately and stores the reference of the cloned file in the cloned object because cloning the original object will not clone it deeply with all of the referenced classes in its fields (to learn more see [this](https://stackoverflow.com/questions/184710/what-is-the-difference-between-a-deep-copy-and-a-shallow-copy)).