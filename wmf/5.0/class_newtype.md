# PowerShell 5.0 中的新语言功能 

PowerShell 5.0 引入了以下 Windows PowerShell 中的新语言元素︰

## 课堂关键字

**类**关键字定义新课程。 这是真正的.NET Framework 类型。 类成员是公共的但仅公共模块范围内。
不能引用为一个字符串类型的名称 (例如，`New-Object`不起作用)，而且在此版本中，您无法使用键入文本 (例如， `[MyClass]`) 外部脚本/模块文件中定义类。

```powershell
class MyClass
{
    ...
}
```

## 枚举关键字和枚举

添加**枚举**关键字的支持，它使用换行符作为分隔符。
当前限制︰ 不能定义枚举本身，但可以初始化列另一个枚举，枚举，下面的示例所示。
此外，当前不能指定基类型;始终是 [int]。

```powershell
enum Color2
{
    Yellow = [Color]::Blue
}
```

枚举值必须是分析时间常量;您不能将其设置为调用的命令的结果。

```powershell
enum MyEnum
{
    Enum1
    Enum2
    Enum3 = 42
    Enum4 = [int]::MaxValue
}
```

枚举支持算术运算，如下面的示例中所示。

```powershell
enum SomeEnum { Max = 42 }
enum OtherEnum { Max = [SomeEnum]::Max + 1 }
```

## 导入 DscResource

**导入 DscResource**现在是正确的动态关键字。
PowerShell 分析指定的模块根模块中，搜索包含**DscResource**属性的类。

## ImplementingAssembly

新字段， **ImplementingAssembly**，已添加到 ModuleInfo。 它设置为如果脚本定义类，对于脚本模块创建动态程序集或加载二进制模块。 未设置何时 ModuleType = 清单。 

反射**ImplementingAssembly**字段上的发现的模块中的资源。 这意味着您可以发现 PowerShell 或其他托管的语言编写的资源。

具有初始值字段︰      

```powershell
[int] $i = 5
```

支持静态;其工作方式的属性，如一样类型约束，以便它可以指定任何顺序。

```powershell
static [int] $count = 0
```

类型是可选的。

```powershell
$s = "hello"
```

所有成员都是公共的。 

## 构造函数和实例化

Windows PowerShell 类可以有构造函数。他们拥有其类相同的名称。 可以重载构造函数。 支持静态构造函数。 运行构造函数中的任何代码之前初始化使用初始化表达式的属性。 静态属性初始化之前正文静态构造函数，并且在非静态构造函数的正文前初始化实例属性。 目前，没有为从另一个构造函数调用构造函数语法 (如 C\#语法": this()")。 解决方法是定义常见的初始化方法。 

下面是此版本中的实例化类的方法。

实例化使用默认构造函数。 请注意，在此版本中不支持新建对象。

```powershell
$a = [MyClass]::new()
```

调用构造函数的参数

```powershell
$b = [MyClass]::new(42)
```

将数组传递给多个参数的构造函数
```powershell
$c = [MyClass]::new(@(42,43,44), "Hello")
```

在此版本中，新建对象不适用于 Windows PowerShell 中定义类。 也为此版本中，键入名称才可见按词汇，指不可见以外的模块或脚本定义类。 函数可以返回的 Windows PowerShell 中定义类实例和实例工作也在模块或脚本之外。

`Get-Member -Static` 列出了构造函数，以便您可以查看重载与任何其他方法。 此语法的性能也是比新建对象速度更快。

命名**新**的伪静态方法处理.NET 类型，如下面的示例中所示。

```powershell
[hashtable]::new()
```

现在，您可以看到构造函数重载与获取的成员，或在此示例中所示︰

```powershell
PS> [hashtable]::new
OverloadDefinitions
-------------------
hashtable new()
hashtable new(int capacity)
hashtable new(int capacity, float loadFactor)
```

## 方法

作为具有仅结束块简言之实现 Windows PowerShell 类方法。 所有方法都是公共的。 下面显示定义名为**DoSomething**的方法的示例。

```powershell
class MyClass
{
    DoSomething($x)
    {
        $this._doSomething($x) # method syntax
    }
    private _doSomething($a) {}
}
```

方法调用︰

```powershell
$b = [MyClass]::new()
$b.DoSomething(42) 
```

重载方法--即，那些名为现有的方法相同，但通过指定的值-区分也受支持。

## 属性 

所有属性都是公共的。 属性需要换行符或分号。 如果不指定了任何对象类型，属性类型是对象。

使用有效性属性或参数转换属性的属性 (例如`[ValidateSet("aaa")]`) 按预期方式工作。

## 隐藏

已添加了新的关键字，**隐藏**。 **隐藏**可以应用于属性和方法 （包括构造函数）。

隐藏的成员是公共的但不会显示在输出中获取成员的除非添加参数是-强制。

隐藏成员未包括完成或使用智能感知，除非完成在定义隐藏的成员课堂中出现的选项卡。

新的属性，以使 C# 代码可以在 Windows PowerShell 中相同的语义已添加**System.Management.Automation.HiddenAttribute** 。

## 返回类型

返回类型是合同;返回值将转换为所需的类型。 如果没有返回指定类型，则返回类型是 void。 没有对象; 无流式处理对象不能写入管道有意或无意。

## 属性

添加了两个新属性、 **DscResource**和**DscProperty** 。

## 变量的词汇设置范围

以下举例说明如何词汇范围的工作方式在此版本中。

```powershell
$d = 42 # Script scope

function bar
{
    $d = 0 # Function scope
    [MyClass]::DoSomething()
}

class MyClass
{
    static [object] DoSomething()
    {
        return $d # error, not found dynamically
        return $script:d # no error
        $d = $script:d
        return $d # no error, found lexically
    }
}

$v = bar
$v -eq $d # true
```

## 端到端示例

下面的示例创建多个新的自定义类实现 HTML 动态样式表语言 (DSL)。 然后，该示例添加帮助程序函数来创建特定元素类型为元素类，如标题样式和表的一部分，因为类型不能使用范围之外的模块。

```powershell
# Classes that define the structure of the document
#
class Html
{
    [string] $docType
    [HtmlHead] $Head
    [Element[]] $Body
    
    [string] Render()
    {
        $text = "<html>`n<head>`n"
        $text += $this.Head
        $text += "`n</head>`n<body>`n"
        $text += $this.Body -join "`n" # Render all of the body elements
        $text += "</body>`n</html>"
        return $text
    }
    [string] ToString() { return $this.Render() }
}

class HtmlHead
{
    $Title
    $Base
    $Link
    $Style
    $Meta
    $Script
    [string] Render() { return "<title>$($this.Title)</title>" }
    [string] ToString() { return $this.Render() }
}

class Element
{
    [string] $Tag
    [string] $Text
    [hashtable] $Attributes
    [string] Render() {
        $attributesText= ""
        if ($this.Attributes)
        {
            foreach ($attr in $this.Attributes.Keys)
            {
                #BUGBUG - need to validate keys against attribute
                $attributesText += " $attr=`"$($this.Attributes[$attr])\`""
            }
        }
        return "<$($this.tag)${attributesText}>$($this.text)</$($this.tag)>`n"
    }
[string] ToString() { return $this.Render() }
}

#
# Helper functions for creating specific element types on top of the classes.
# These are required because types aren’t visible outside of the module.
#

function H1 { [Element] @{ Tag = "H1" ; Text = $args.foreach{$_} -join " " }}
function H2 { [Element] @{ Tag = "H2" ; Text = $args.foreach{$_} -join " " }}
function H3 { [Element] @{ Tag = "H3" ; Text = $args.foreach{$_} -join " " }}
function P { [Element] @{ Tag = "P" ; Text = $args.foreach{$_} -join " " }}
function B { [Element] @{ Tag = "B" ; Text = $args.foreach{$_} -join " " }}
function I { [Element] @{ Tag = "I" ; Text = $args.foreach{$_} -join " " }}
function HREF
{
    param (
        $Name,
        $Link
    )
    return [Element] @{
        Tag = "A"
        Attributes = @{ HREF = $link }
        Text = $name
    }
}
function Table
{
    param (
    [Parameter(Mandatory)]
    [object[]]
        $Data,
    [Parameter()]
    [string[]]
        $Properties = "*",
    [Parameter()]
    [hashtable]
        $Attributes = @{ border=2; cellpadding=2; cellspacing=2 }
    )
$bodyText = ""
# Add the header tags
$bodyText += $Properties.foreach{TH $_}
# Add the rows
$bodyText += foreach ($row in $Data)
    {
        TR (-join $Properties.Foreach{ TD ($row.$\_) } )
    }

    $table = [Element] @{
        Tag = "Table"
        Attributes = $Attributes
        Text = $bodyText
    }
$table
}
function TH { ([Element] @{ Tag = "TH" ; Text = $args.foreach{$_} -join " " }) }
function TR { ([Element] @{ Tag = "TR" ; Text = $args.foreach{$_} -join " " }) }
function TD { ([Element] @{ Tag = "TD" ; Text = $args.foreach{$_} -join " " }) }
function Style

{
    return [Element] @{
        Tag = "style"
        Text = "$args"
    }
}

# Takes a hash table, casts it to and HTML document
# and then returns the resulting type.
#
function Html ([HTML] $doc) { return $doc }
```