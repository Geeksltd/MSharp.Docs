# Standard vs custom CSS

## Problem

You want to compare different approaches toward website design and layout in M# to make an informed decision about using CSS in your website application.

## Approaches

You have 3 choices regarding the website design:

1- You want to create your application rapidly, so you left styles as default and do not use any CSS related methods in your M# model.

2- You want to change some elements of design and layout in a limited way. You either change the styles from the existing CSS framework or add your CSS library.

3- Your website has a lot of unique UI/UX features and should have its own customized layout and design while ensuring consistency. This approach should be chosen with care as it requires a lot of effort and needs having UI/UX designers in your team.

### Supported CSS frameworks
M# natively support some common libraries like [Font Awesome](https://fontawesome.com/) and [Bootstarap](https://getbootstrap.com/), so you can use styles and classes from these libraries right away from CSS related methods in the model classes. 

Other libraries can be added as described [here](https://www.msharp.co.uk/#/how-to/javascript/addingLibrary).

### Using Sass
Using a preprocessor is a vital part of a modern CSS workflow. It helps a lot for maintaining your codebases for styles as it gets larger and more complex. One of the most popular preprocessors is [Sass](https://sass-lang.com/) which is also used in the M# project template.

For using Sass to create your custom styles, you should create your styles in the Sass files with the `.scss` file extension, then add their references to the `styles.scss` file and run the `sass-to-css.bat` file to build your Sass files.

### Organizing custom styles 
The key to managing styles in a large website is using separation of concerns and modular CSS. This ensures that modifying a style wouldn't create undesirable side effects. 

In modular CSS we do not add styles to the element type as a whole or for a specific Id. Always styles should be added to the classes instead. Styles definition must be at the most detailed level possible to prevent accidental styling of unwanted other items (like `customer-detail .form .item {…}`) 

The best practices for placing the style file is as follows: 

- Add only global theme-related and generic styles to `Common/styles.scss`.
- Add only high-level layout related styles to `Blank.scss` and other theme level Sass files (if applicable).
- Create several individual Saas files per module or feature of the application and place them inside a folder with the module name.

In the microservice architecture, the Access Hub service usually contain the CSS theme and general layout code, that is indirectly used by all feature microservices. So the first two of the above will be placed in Access Hub.