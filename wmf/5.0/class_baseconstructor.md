# 呼叫基类构造函数

若要从子类呼叫基类构造函数中使用关键字**基**︰

```PowerShell
class A 
{
    [int]$a

    A([int]$a)
    {
        $this.a = $a
    }
}

class B : A
{
    B() : base(103) {}
}

[B]::new().a # return 103
```

如果基类具有默认 （无参数） 构造函数，您可以省略显式构造函数调用︰

```PowerShell
class C : B
{
    C([int]$c) {}
}
```