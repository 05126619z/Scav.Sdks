# R.E.P.O. Common Build SDK
[![GitHub](https://img.shields.io/badge/GitHub-%23121011.svg?logo=github&logoColor=white)](https://github.com/linkoid/Repo.Sdks/tree/main/Common.Build#Repo-Common-Build-SDK)
[![Stars](https://img.shields.io/github/stars/linkoid/Repo.Sdks)](https://github.com/linkoid/Repo.Sdks/stargazers)
[![License](https://img.shields.io/github/license/linkoid/Repo.Sdks)](https://github.com/linkoid/Repo.Sdks/tree/main?tab=MIT-1-ov-file)

[![R.E.P.O. Modding](https://custom-icon-badges.demolab.com/badge/R.E.P.O.-Modding-FCD233.svg?labelColor=black&logo=repogame)](https://github.com/zelofi/REPOModdingGuide/wiki)
[![dotnet](https://img.shields.io/badge/dotnet-512BD4?logo=dotnet)](https://dotnet.microsoft.com/en-us/download)
[![MSBuild](https://custom-icon-badges.demolab.com/badge/MSBuild-B35601.svg?logo=msbuild)](https://learn.microsoft.com/en-us/visualstudio/msbuild/msbuild)

Provides minimal MSBuild properties for finding a 
R.E.P.O. installation on the local machine and other misc. targets.

To use this package, add a package reference to the project:
```xml
<PackageReference Include="Linkoid.Repo.Common.Build" Version="*" PrivateAssets="all" />
```

## MSBuild Properties
* `$(GameDirectory)`: The path to the local installation of R.E.P.O.
* `$(BepInExDirectory)`: The path to the BepInEx directory inside R.E.P.O.
* See the source code on github for more properties that are available to targets.

## Directory Repo Props & Targets Files
Whenever this package is used, it automatically loads the first
`Directory.Repo.props` and `Directory.Repo.targets`
files that are found in any of the directories above the project.
This can be used to manually specify a custom game directory for a
project/all projects in a directory and it's subdirectories.
Even if R.E.P.O. can be found automatically, it can be overriden
to use a special version/installation of the game.

Here is an example `Directory.Repo.props` file:
```xml
<Project>
  <PropertyGroup>
    <GameDirectory>C:\Path\To\REPO\</GameDirectory>
    <StartArguments>--doorstop-enable true --doorstop-target "%AppData%\com.kesomannen.gale\repo\profiles\Default\BepInEx\core\BepInEx.Preloader.dll" --gale-profile "Default"</StartArguments>
  </PropertyGroup>
</Project>
```
