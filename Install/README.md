# Installing MSharp

## Prerequisites

Make sure you have all of the following installed on your computer:

1. Windows 10
2. Visual Studio 2017 (Latest build)
3. GIT for Windows ([Install from here](http://gitforwindows.org/))
4. NodeJS for Windows ([Install from here](https://nodejs.org/en/download/))
5. Yarn Package Manager ([Install from here](https://yarnpkg.com/latest.msi))
6. Install **Bower** by typing `npm install -g bower` in the **CMD** or **Git Bash**
7. Docker, plus Windows runtime ([Install from here](https://docs.docker.com/toolbox/toolbox_install_windows/))
8. An instance of SQL Server ([Install from here](https://www.microsoft.com/en-us/sql-server/sql-server-downloads))
9. SSMS (Recommended not required [Install from here](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017))

## How to install

1. Close all instances of Visual Studio.
2. Install all M# Visual Studio extensions [from here](https://marketplace.visualstudio.com/search?term=msharp&target=VS&category=All%20categories&vsVersion=&sortBy=Relevance)
3. Open your Visual Studio as **ADMINISTRATOR** (It's recommended that you make this the default.)

## Create your first application

1. In Visual Studio, create a new project.
2. On the left hand side, select **.NET Core** as the category.
3. On the right hand side, select **M# - ASP.NET Core** as the template type, then click on **Create**.
4. On the next page, leave the default settings as it is, and click **Create** again.(Read the note below)
5. Set **Website** as your start-up project.
6. Go to `appsettings.json` and verify the connection string.
7. Run the app to see the login page.

### Note

> At this stage, it will download the latest project template [from here](https://github.com/Geeksltd/Olive.MvcTemplate) and replace the name placeholder with your specified app name. It will also run the **Build.bat** file from the solution root directory which will install yarn's packages, compite CSS and TypeScript files, etc.

## Troubleshooting

If you experienced any problem try the following:

1. Open a `CMD` with administrator permission and run `Build.bat` file and watch for errors. You might have missing components.
2. Make sure all nuget packages are successfully restored.
3. If your package did not restore correctly, remove the .nuget contents folder from `C:\Users\{YOUR USER NAME}`
4. Make sure that the path to the solution is not too long or it does not contain special characters such as space. (It's suggested that you create all project in the `C:\Project\` path.)
5. If you had any kind of difficulties and unexpected problems or you faced with M#/Olive template issues, just leave an issue [HERE](https://github.com/Geeksltd/Olive.MvcTemplate/issues).
