# 调用基类方法

在子类别中的现有方法，可以覆盖。 若要执行此操作，请使用相同的名称和签名声明方法︰

```PowerShell
class baseClass
{
    [int]foo() {return 100500}
}

class childClass1 : baseClass
{
    [int]foo() {return 200600}
}

[childClass1]::new().foo() # return 200600
```

若要从重写实现调用基类方法，强制转换为基类 ([baseClass] $这) 调用上︰

```PowerShell
class childClass2 : baseClass
{
    [int]foo()
    {
        return 3 * ([baseClass]$this).foo()
    }
}

[childClass2]::new().foo() # return 301500
```

所有 PowerShell 方法都是虚拟。 您可以通过使用相同的语法，如您执行操作的替代隐藏错误的非虚拟.NET 方法︰ 只需声明具有相同名称和签名的方法。

```PowerShell
class MyIntList : system.collections.generic.list[int]
{
    # Add is final in system.collections.generic.list
    [void] Add([int]$arg)
    {
        ([system.collections.generic.list[int]]$this).Add($arg * 2)
    }
}

$list = [MyIntList]::new()
$list.Add(100)
$list[0] # return 200
```