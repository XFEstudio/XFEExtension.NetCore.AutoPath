# XFEExtension.NetCore.AutoPath

## 描述

自动路径创建工具，自动创建不存在的文件夹，对路径统一管理

## 自动实现路径管理

#### 基础用法

```csharp
//创建路径管理类
public partial class AppPath
{
    [AutoPath]
    readonly static string myTestPath = "MyTestPath/Test";
    [AutoPath]
    readonly static string mySecTestPath = $"{MyTestPath}/Sec";//路径可以引用自动生成的路径
}


//使用统一管理的路径
class Program
{
    static void Main(string[] args)
    {
        File.WriteAllText($"{AppPath.MyTestPath}/test.txt", "Hello World");//此时如果没有MyTestPath则会自动创建
        var exist = Directory.Exists(AppPath.MySecTestPath);
        Console.WriteLine(exist);//结果为True
    }
}
```

#### 为路径添加注释

```csharp
public partial class AppPath
{
    /// <summary>
    /// 测试路径
    /// 这段注释会自动添加至自动生成的Name属性上
    /// </summary>
    [AutoPath]
    readonly static string myTestPath = "MyTestPath/Test";
    [AutoPath]
    readonly static string mySecTestPath = $"{MyTestPath}/Sec";
}
```

#### 使用部分方法来设置get方法

```csharp
public partial class AppPath
{
    [AutoPath]
    readonly static string myTestPath = "MyTestPath/Test";
    [AutoPath]
    readonly static string mySecTestPath = $"{MyTestPath}/Sec";

    static partial void GetMyTestPathProperty()
    {
        Console.WriteLine("获取了MyTestPath");
    }
}
```