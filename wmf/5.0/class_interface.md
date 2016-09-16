# 声明实现的接口

未指定的基本类型时，可以之后基类型，或冒号 （:） 后立即声明实现的接口。 使用逗号分隔所有类型的名称。 它是非常类似于 C# 语法。

```PowerShell
class MyComparable : system.IComparable
{
    [int] CompareTo([object] $obj)
    {
        return 0;
    }
}

class MyComparableBar : bar, system.IComparable
{
    [int] CompareTo([object] $obj)
    {
        return 0;
    }
}
```