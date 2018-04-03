# File
M# File is a high level representation of a Document. By adding a File property, M# will generates a C# Document property with its XML documentation. M# gives you flexibility by using some specific File methods allowing you to change the behaviour in your C# logic.

## Creation
M# has two file related methods:
- SecureFile()
- SecureImage()

## Methods

| Methods                                | Sample                                               | Description                                                                                                                   |
|:---------------------------------------|:-----------------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------|
| .AutoOptimize(bool)       | ```SecureImage("Photo") .AutoOptimize();```     | Auto optimize will have no effect on the database column definition. If set to "True" M# will optimize your image by calling the method `OptimizeImage(800, 600, 75)` in your property setter. "800" is the width, "600" the height and "75" the optimization quality. This will reduce the dimensions of your image and the size of the file. |
| .IsImage(bool)            | ```SecureImage("Photo") .IsImage();```                      | Is image will have no effect on the database column definition. This method pre-populates other methods related to images, like the size and optimization. |
| .DefaultValueUrl(string value)         | SecureImage("Photo") .DefaultValueUrl("//website.com/logo.png"); | Default value url will have no effect on the database column definition or the generated C# class. It is only used in ASP.Net pages, if there is no image provided for the instance M# will use this value as the default image. |
| .Height(int? value)                    | SecureImage("Photo") .AutoOptimize() .Height(600);     | Height will have no effect on the database column definition. Set to 600 and used with the "Auto optimize" method, this will reduce the size of your image if its height is more than 600 pixels. The `OptimizeImage()` method is called in the property setter to perform this operation. |
| .OptimizationQuality(int? value)       | SecureImage("Photo") .AutoOptimize() .OptimizationQuality(50); | Optimization quality will have no effect on the database column definition. Set to 50 and used with the "Auto optimize" method, this will reduce the quality of your image by 50%. The `OptimizeImage()` method is called in the property setter to perform this operation. |
|.PreserveTransparency(bool value = true)|SecureImage("Photo") .AutoOptimize() .PreserveTransparency();| Preserve transparency will have no effect on the database column definition. Used with the "Auto optimize" method, this will keep the transparency in all images. The `OptimizeImage()` method is called in the property setter to perform this operation. |
| .ValidExtensions(string value)         | SecureImage("Photo") .ValidExtensions("jpg, png, bmp"); | Valid extensions will have no effect on the database column definition. It is important to specify valid extensions for files to avoid some incompatibility or security problems. Enter a comma separated list of valid extensions and M# will generate a validation rule that checks the extension of the file. |
| .Width(int? value)                     | SecureImage("Photo") .AutoOptimize() .Width(800);      | Width will have no effect on the database column definition. When set to 800 and used with the "Auto optimize" method, this will reduce the size of your image if its width is more than 800 pixels. The `OptimizeImage()` method is called in the property setter to perform this operation. |
