# Handling files and documents

## problem

When we need to receive files from a user, we need to allow them to upload it in a form.
The form should have a field for uploading the file and accept it if the file is appropreate.

## Implementation

The `SecureFile()` property can be used in an entity so the form using it will allow the user to upload a file.
The file will be stored on the disk in a configurable folder and the address of the file will be stored in the database table.

