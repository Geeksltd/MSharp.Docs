# Allowed file extensions

## Problem

When you allow users to uplaod files to your website, you usually only can process a limited set of formats.
Also from a security point of view, it is not a good idea to allow users to upload any type of arbitrary file to the web application.
M# allows you to choose the valid extensions of the files when you insert an upload control in a page.

## Implementation

Let's define a product page which allows the user to upload an image of the product with its name to the server.
Then we will limit the accepted formats to png and bmp.

```csharp

```