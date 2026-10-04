# Setting up for local nuget packages

## Overall Setup Steps

1. Make a folder where the packages (`*.nupkg` files) will be placed.
    - In this example it is called "LocalPackages"
2. Method A: When adding the package, pass the folder as argument.
    - In this example project, to add `./LocalPackages/serilog.4.4.0.nupkg`, call `dotnet add package serilog --source ./LocalPackages`
    - This example project also needs `./LocalPackages/serilog.sinks.console.6.1.1.nupkg`
3. Method B: Add `<PropertyGroup><RestoreSources>./LocalPackages</RestoreSources></PropertyGroup>` to the `.csproj` file to force always using local packages (refer to `demo.csproj`)
    - NOTE: I couldn't get this example to work: https://stackoverflow.com/a/44463578 - dotnet would always try the online source first, fail, and then stop, even when the order of the sources was changed.

## Notes / Gotchas

1. When testing whether local install works, make sure to call `dotnet nuget locals all --clear`to make sure the nuget cache isn't being accidentally used to fetch the package, invalidating your test results.

2. With Method B, you can just do `dotnet run` and it should find the package automatically.
    - It is also recommended to test that you can fail as well as pass (incase you are always using the online or cached version by accident), by removing the package files from the package folder.