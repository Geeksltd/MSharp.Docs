# ChangeLog
### 5.2.XXX
#### 5.2.211 (4 November  2021): Pangloin page model
 
Added a feature in M# to generate page model for all elements in UI for a project for being used in Pangolin test cases in order to:
- Quicker to write pangolin tests
- Cleaner and more reliable tests
- Faster end results due to compile time checking
- More enjoyable to write and change
- Enables instantaneous test coverage report to know which application pages and modules are not touched by the tests

#### 5.2.209 (25 October  2021): Bug fix
 
Added the 'generated code' mark above the generated files for some missing files for being skipped from code analysis.
#### 5.2.206 (1 October  2021): Bug fix
 
Fixed the generated code for `Parse` method for the  classes inherited from the enum entity type.

#### 5.2.205 (29 September 2021): Bug fix

Fixed the generated code for `ControlCssClass` method, before fixing the double quotation mark(") in the argument for razor code was changed.
