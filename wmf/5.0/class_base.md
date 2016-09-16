# 声明基类
您可以将 Windows PowerShell 类声明为另一个 Windows PowerShell 类的基本类型。

```PowerShell
class bar
{
   [int]foo() 
       {
           return 100500
       }
}

class baz : bar {}

[baz]::new().foo() # return 100500
```

您还可以为基类使用现有的.NET Framework 类型︰

```PowerShell
class MyIntList : system.collections.generic.list[int]
{
    
}

$list = [MyIntList]::new()

$list.Add(100)

$list[0] # return 100
```