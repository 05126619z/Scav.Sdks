# R.E.P.O. Plugin Build SDK
[![GitHub](https://img.shields.io/badge/GitHub-%23121011.svg?logo=github&logoColor=white)](https://github.com/linkoid/Repo.Sdks/tree/main/Plugin.Build#Repo-Plugin-Build-SDK)
[![Stars](https://img.shields.io/github/stars/linkoid/Repo.Sdks)](https://github.com/linkoid/Repo.Sdks/stargazers)
[![License](https://img.shields.io/github/license/linkoid/Repo.Sdks)](https://github.com/linkoid/Repo.Sdks/tree/main?tab=MIT-1-ov-file)

[![R.E.P.O. Modding](https://custom-icon-badges.demolab.com/badge/R.E.P.O.-Modding-FCD233.svg?labelColor=black&logo=repogame)](https://github.com/zelofi/REPOModdingGuide/wiki)
[![dotnet](https://img.shields.io/badge/dotnet-512BD4?logo=dotnet)](https://dotnet.microsoft.com/en-us/download)
[![MSBuild](https://custom-icon-badges.demolab.com/badge/MSBuild-B35601.svg?logo=msbuild)](https://learn.microsoft.com/en-us/visualstudio/msbuild/msbuild)

Provides MSBuild properties and targets for building and running a R.E.P.O. plugin.

## Usage
To use this package, add a package reference to the project:
```xml
<ItemGroup>
	<PackageReference Include="Linkoid.Repo.Common.Build" Version="*" PrivateAssets="all" />
</ItemGroup>
```

Use a NuGet Package to include game libraries, or enable automatic game references
```xml
<PropertyGroup>
	<EnableGameReferences>true</EnableGameReferences>
</PropertyGroup>
```

If automatic game references cannot be resolved, setup a `Directory.Repo.props` file.
Information regarding how to setup Directory.Repo.props can be found in the 
[Common Build SDK README](https://github.com/linkoid/Repo.Sdks/tree/main/Common.Build#readme).

## Features
* Automatically locates local R.E.P.O. installation with [Repo.Common.Build](https://github.com/linkoid/Repo.Sdks/tree/main/Common.Build#Repo-Common-Build-SDK).
* Built plugin is copied to the plugins folder of the target game.
* Configures debug symbols to hide parent path and be compatible with mono.
* The IDE's play button / `dotnet run` will start the game.
* Does not bundle or transitively reference any assemblies.
  * Can easily be added to existing projects that already have their own references.
  * Can specify to reference local game assemblies if not using GameLibs packages.

## MSBuild Properties
* `<PluginName>`
  * The thunderstore safe name for the plugin.
  * Default: `$(MSBuildProjectName)` with common invalid characters removed
* `<StartGameOnRun>`
  * Start the game when using play button or `dotnet run`.
  * Default: `true` 
* `<EnableGameReferences>`
  * Add game assembly references from the local game installation. 
  * Default: `false`
* `<EnableUnityReferences>`
  * Add Unity assembly references from the local game installation.
  * Default: use value of EnableGameReferences
* `<CopyFilesToPluginOutputDirectoryOnBuild>`
  * Copy the plugin to the game's plugin folder after it's built.
  * Default: `true`
* `<CopyFilesToPluginOutputDirectoryOnRun>`
  * Copy the plugin to the game's plugin folder right before the game is run.
  * Default: `true`
* `<PluginOutputSubdirectory>`
  * The path relative to BepInEx/plugins/ to which the plugin will be copied.
  * Default: `$(Authors)-$(PluginName)` or `$(PluginName)`
* See additional configurable properties inherited from [Repo.Common.Build](https://github.com/linkoid/Repo.Sdks/tree/main/Common.Build#MSBuild-Properties).

## MSBuild Item Metadata
### CopyToPluginOutputDirectory
Anything copied to the build output directory will also be copied to the 
plugin output. It is possible to also specify items that aren't copied 
to the output directory to also be copied to plugin output.
```xml
<ItemGroup>
  <None Include="NOTICE.txt" CopyToPluginOutputDirectory="Always" />
</ItemGroup>
```

By default, the following files are copied to the plugin output if they are found:
* README.md
* README.txt
* manifest.json
* icon.png

This behaviour can be overriden by explicitly specifying not to copy these files.
```xml
<ItemGroup>
  <None Update="README.txt" CopyToPluginOutputDirectory="Never" />
</ItemGroup>
```

## Example
An example of using this SDK can be seen in the [Plugin Build Test Project](https://github.com/linkoid/Repo.Sdks/blob/main/Plugin.Build.Tests/Plugin.Build.Tests.csproj).
