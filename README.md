Repro showing that hot reload doesn't work in this case.

## Hot reloading not working

Clone this repo, then in a powershell terminal go to the directory containing the file `ReactApp.sln`.

Then execute
```
dotnet restore
```

Then go to subdirectory `ClientApp` and execute the following:
```
npm ci
```
Do no use npm install to avoid changing `package-lock.json`.

Then open the solution in Visual Studio 2019 Community Edition, version 16.4.2

When starting the ReactApp project, everything is fine, except that hot reload doesn't work in our dev environment.

Changing a file like `ClientApp/src/components/Home.js` is reflected when reloading the page in the browser.

However, it appears as if the development service is not started properly or at all, so hot reload doesn't work.

## Hot reloading working

In the powershell terminal mentioned above, run the command ```npm run start```

Now, when you modify a file like `ClientApp/src/components/Home.js` works.

## Hypothesis

The code base in this repo was created using 
```
dotnet new react
```
after installing the templates using 
```
dotnet new -install "Microsoft.AspNetCore.SpaTemplates::*"
```
Then all npm package listed in `package.json` where updated.

Finally, to resolve any possilbe vulnerabilities, the following command was used in folder `ClientApp`:
```
npm audit fix
```
