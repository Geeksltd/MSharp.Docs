# Installing MSharp

## Prerequisites

Make sure you have all of the following installed on your computer:

1. Windows 10
2. Visual Studio 2019 (Latest build)
3. GIT for Windows ([Install from here](http://gitforwindows.org/))
3. .NET Core SDK ([Install from here](https://dotnet.microsoft.com/download/dotnet-core/3.1))
4. NodeJS for Windows ([Install from here](https://nodejs.org/en/download/))
5. Yarn Package Manager ([Install from here](https://yarnpkg.com/latest.msi))
6. An instance of SQL Server ([Install from here](https://www.microsoft.com/en-us/sql-server/sql-server-downloads))
7. SSMS (Recommended not required [Install from here](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017))

## How to install

1. Run `dotnet tool install --global msharp-build`
2. Run cmd in admin mode and execute `powershell.exe -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))"`
3. Run cmd in admin mode and execute `msharp-build /tools`
4. Close all instances of Visual Studio.
5. Install all M# Visual Studio extensions [from here](https://marketplace.visualstudio.com/search?term=msharp&target=VS&category=All%20categories&vsVersion=&sortBy=Relevance)
6. Open your Visual Studio as **ADMINISTRATOR** (It's recommended that you make this the default.)

## Create your first application

1. Open a command prompt and `cd` into ** C:\Projects\ ** or whereever your projects usually are.
2. Run `msharp-build /new /n:MyProjectName` changing *MyProjectName* to your actual project name ([learn more](https://github.com/Geeksltd/msharp-build))
3. Open the generated solution in Visual Studio.
5. Set **Website** as your start-up project.
6. Go to `appsettings.json` and verify the connection string.
7. Run the app to see the login page.

## Troubleshooting

If you experienced any problem try the following:

1. Open a `CMD` with administrator permission and run `Build.bat` file and watch for errors. You might have missing components.
2. Make sure all nuget packages are successfully restored.
3. If your package did not restore correctly, remove the .nuget contents folder from `C:\Users\{YOUR USER NAME}`
4. Make sure that the path to the solution is not too long or it does not contain special characters such as space. (It's suggested that you create all project in the `C:\Project\` path.)
5. If you had any kind of difficulties and unexpected problems or you faced with M#/Olive template issues, just leave an issue [HERE](https://github.com/Geeksltd/Olive.MvcTemplate/issues).
