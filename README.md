Repro showing that hot reload doesn't work in this case.

## Hot reloading not working

1. In a powershell terminal go to the directory containing the file `ReactApp.sln`.

2. Then execute ```dotnet restore```

3. Go to subdirectory `ClientApp` and execute ```npm ci``` Do no use npm install to avoid changing `package-lock.json`.

4. Open the solution in Visual Studio 2019 Community Edition, version 16.4.2

5. When starting the ReactApp project, everything is fine, except that hot reload doesn't work in our dev environment.

6. Changing a file like `ClientApp/src/components/Home.js` is reflected when reloading the page manually in the browser.

7. However, it appears as if the development service is not started properly or at all, so hot reload doesn't work.

## Hot reloading working

1. In the powershell terminal mentioned above, run the command ```npm run start```

2. Now, modifying a file like `ClientApp/src/components/Home.js` causes hot reload

## Hypothesis

The code base in this repo was created as follows:

1. Install template: ```dotnet new -install "Microsoft.AspNetCore.SpaTemplates::*"```

2. Create directory `ReactApp`

3. Within directory `ReactApp` run ```dotnet new react```

4. Within directory `ClientApp` update all npm depencencies to latest stable (as of writing)

5. Execute ```npm audit fix``` to ensure all vulnerabilities are resolved

6. This updates all react related npm packages as well. Perhaps this requires a change in the SpaServices.Extensions for React.

## Environment

- Visual Studio 2019 Community Edition, version 16.4.2
- Nodejs version 12.13.1
- .NET Core 3.1

Output of ```dotnet --info```:

```
.NET Core SDK (reflecting any global.json):
 Version:   3.1.100
 Commit:    cd82f021f4

Runtime Environment:
 OS Name:     Windows
 OS Version:  10.0.18362
 OS Platform: Windows
 RID:         win10-x64
 Base Path:   C:\Program Files\dotnet\sdk\3.1.100\

Host (useful for support):
  Version: 3.1.0
  Commit:  65f04fb6db

.NET Core SDKs installed:
  3.1.100 [C:\Program Files\dotnet\sdk]

.NET Core runtimes installed:
  Microsoft.AspNetCore.All 2.1.14 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.All]
  Microsoft.AspNetCore.App 2.1.14 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
  Microsoft.AspNetCore.App 3.1.0 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
  Microsoft.NETCore.App 2.1.14 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
  Microsoft.NETCore.App 3.1.0 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
  Microsoft.WindowsDesktop.App 3.1.0 [C:\Program Files\dotnet\shared\Microsoft.WindowsDesktop.App]

To install additional .NET Core runtimes or SDKs:
  https://aka.ms/dotnet-download
```
