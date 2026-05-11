# XFEExtension.NetCore.AutoPath

[![NuGet](https://img.shields.io/nuget/v/XFEExtension.NetCore.AutoPath?label=NuGet&logo=NuGet)](https://www.nuget.org/packages/XFEExtension.NetCore.AutoPath/)
[![NuGet Downloads](https://img.shields.io/nuget/dt/XFEExtension.NetCore.AutoPath?label=Downloads&logo=NuGet)](https://www.nuget.org/packages/XFEExtension.NetCore.AutoPath/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE.txt)
[![.NET](https://img.shields.io/badge/.NET-10.0-512BD4)](https://dotnet.microsoft.com/download)

> 📖 English | [简体中文](https://github.com/XFEstudio/XFEExtension.NetCore.AutoPath/blob/master/README.zh-CN.md)

## Description

An automatic path creation tool that automatically creates non-existent folders and provides unified path management.

## Auto Path Management

#### Basic Usage

```csharp
// Create a path management class
public partial class AppPath
{
    [AutoPath]
    readonly static string myTestPath = "MyTestPath/Test";
    [AutoPath]
    readonly static string mySecTestPath = $"{MyTestPath}/Sec"; // Paths can reference auto-generated paths
}


// Use the unified path management
class Program
{
    static void Main(string[] args)
    {
        File.WriteAllText($"{AppPath.MyTestPath}/test.txt", "Hello World"); // MyTestPath will be auto-created if it does not exist
        var exist = Directory.Exists(AppPath.MySecTestPath);
        Console.WriteLine(exist); // Output: True
    }
}
```

#### Add Comments to Paths

```csharp
public partial class AppPath
{
    /// <summary>
    /// Test path
    /// This comment will be automatically added to the auto-generated Name property
    /// </summary>
    [AutoPath]
    readonly static string myTestPath = "MyTestPath/Test";
    [AutoPath]
    readonly static string mySecTestPath = $"{MyTestPath}/Sec";
}
```

#### Use Partial Methods to Set the Get Method

```csharp
public partial class AppPath
{
    [AutoPath]
    readonly static string myTestPath = "MyTestPath/Test";
    [AutoPath]
    readonly static string mySecTestPath = $"{MyTestPath}/Sec";

    static partial void GetMyTestPathProperty()
    {
        Console.WriteLine("MyTestPath was accessed");
    }
}
```
