# Installing M#

## Prerequisites
Make sure you have all of the following installed on your computer:

1. Windows 10
2. Visual Studio 2017 (latest build)
3. GIT for Windows ([install from here](http://gitforwindows.org/))
4. Yarn Package Manager ([install from here](https://yarnpkg.com/latest.msi))

## How to install
1. Close all instances of Visual Studio.
1. Install the MSharp Visual Studio Extension [from here](https://marketplace.visualstudio.com/items?itemName=Paymon.MSharp)
2. Install the MSharp.F7 Visual Studio Extension [from here](https://marketplace.visualstudio.com/items?itemName=Paymon.SmartF7)
3. Open your Visual Studio as ADMIN (it's recommended that you make this the default)

## Create your first application

1. In Visual Studio, click to create a new project.
2. On the left hand side, select ".NET Core" as the category.
3. On the right hand side, select "M# - ASP.NET Core" as the template type.
4. Click Create. On the next page accept the default and click Create again.

### Note
>At this stage, it will download the latest project template [from here](https://github.com/Geeksltd/Olive.MvcTemplate) and replace the name placeholder with your specified app name. It will also run the Initialize.bat file from the solution root directory which will install the NodeJs packages, Gulp, etc.

5. Set Website as your start-up project.
6. Run the app to see the login page.

## Troubleshooting
If you experienced any problem try the following:
1. Open a cmd and run Initialize.bat file and watch for NodeJS error. You might have missing components.
2. Make sure all nuget packages are successfully restored.

### NodeJS / Gulp problems?
If you see errors related to NPM or gulp, it could be that your NodeJs installation is old or corrupted. In that case:
1. Close all Visual Studio instances.
2. Go to Control Panel > Programs and Features. Uninstall Node.
3. From C:\Users\{...}\AppData\Roaming delete the NPM and NPM-CACHE folders.
4. Install NodeJS from https://nodejs.org/en/download/
5. Open a new CMD and run Initialize.bat again.
