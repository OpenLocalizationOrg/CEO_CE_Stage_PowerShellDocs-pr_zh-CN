---
title: "使用静态类和方法"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 418ad766-afa6-4b8c-9a44-471889af7fd9
ms.openlocfilehash: 1d8b45bbfe14bdca7ddfa3fd26d1e66a0a82efbc
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 使用静态类和方法
通过使用**新建对象**，可以创建并不是所有.NET Framework 类。 例如，如果您尝试使用**新建对象**创建**个数**或**System.Math**对象时，您将收到以下错误消息︰

```
PS> New-Object System.Environment
New-Object : Constructor not found. Cannot find an appropriate constructor for
type System.Environment.
At line:1 char:11
+ New-Object  <<<< System.Environment
PS> New-Object System.Math
New-Object : Constructor not found. Cannot find an appropriate constructor for
type System.Math.
At line:1 char:11
+ New-Object  <<<< System.Math
```

因为没有方法以从这些类创建一个新的对象，会出现以下错误。 这些类是引用库的方法和属性不会更改状态。 您不需要创建它们，您只需使用它们。 类和方法如这些被称为*静态类别*，因为它们不会创建、 破坏，或更改。 若要使此清除我们将提供使用静态类别的示例。

### 获取环境数据的个数
通常情况下，使用 Windows PowerShell 中的对象的第一步是使用获取成员以了解哪些它包含的成员。 通过使用静态类别的流程是稍有不同，因为实际课堂不是一个对象。

#### 静态个数课堂引用
您可以通过周围的课程名称用方括号引用静态课堂。 例如，您可以将**个数**参考通过键入括号内的名称。 这样做会显示一些通用类型信息︰

```
PS> [System.Environment]

IsPublic IsSerial Name                                     BaseType
-------- -------- ----                                     --------
True     False    Environment                              System.Object
```

> [!NOTE]
> 如我们前文所述，Windows PowerShell 自动前面添加**系统。** 若要使用**新对象**时，请键入名称。 使用括号中的键入名称，以便您可以指定情况同样的目的**\[个数]**为**\[环境]**。

**个数**类包含有关工作环境当前进程，这是 powershell.exe Windows PowerShell 中工作时的常规信息。

如果您尝试通过键入**查看详细信息，此类\[个数] |获取成员**，对象类型报告为**System.RuntimeType** ，不**个数**︰

```
PS> [System.Environment] | Get-Member

   TypeName: System.RuntimeType
```

若要查看与获取成员的静态成员，指定**静态**的参数︰

```
PS> [System.Environment] | Get-Member -Static

   TypeName: System.Environment

Name                       MemberType Definition
----                       ---------- ----------
Equals                     Method     static System.Boolean Equals(Object ob...
Exit                       Method     static System.Void Exit(Int32 exitCode)
...
CommandLine                Property   static System.String CommandLine {get;}
CurrentDirectory           Property   static System.String CurrentDirectory ...
ExitCode                   Property   static System.Int32 ExitCode {get;set;}
HasShutdownStarted         Property   static System.Boolean HasShutdownStart...
MachineName                Property   static System.String MachineName {get;}
NewLine                    Property   static System.String NewLine {get;}
OSVersion                  Property   static System.OperatingSystem OSVersio...
ProcessorCount             Property   static System.Int32 ProcessorCount {get;}
StackTrace                 Property   static System.String StackTrace {get;}
SystemDirectory            Property   static System.String SystemDirectory {...
TickCount                  Property   static System.Int32 TickCount {get;}
UserDomainName             Property   static System.String UserDomainName {g...
UserInteractive            Property   static System.Boolean UserInteractive ...
UserName                   Property   static System.String UserName {get;}
Version                    Property   static System.Version Version {get;}
WorkingSet                 Property   static System.Int64 WorkingSet {get;}
TickCount                               ExitCode
```

现在，我们可以选择要从个数查看属性。

#### 显示静态属性的个数
个数的属性也是静态的并且必须以不同方式比普通属性中指定。 我们使用**::**来指示到我们要使用的静态方法或属性的 Windows PowerShell。 若要查看用于启动 Windows PowerShell 命令，我们通过键入检查**命令行**属性︰

```
PS> [System.Environment]::Commandline
"C:\Program Files\Windows PowerShell\v1.0\powershell.exe"
```

若要检查的操作系统版本，请通过键入显示 OSVersion 属性︰

```
PS> [System.Environment]::OSVersion

           Platform ServicePack         Version             VersionString
           -------- -----------         -------             -------------
            Win32NT Service Pack 2      5.1.2600.131072     Microsoft Windows...
```

我们可以检查计算机是否正在关闭通过显示**HasShutdownStarted**属性︰

```
PS> [System.Environment]::HasShutdownStarted
False
```

### 执行数学与 System.Math
System.Math 静态类可用于执行一些数学运算。 **System.Math**重要成员是大部分方法，我们可以通过使用**获取成员**显示。

> [!NOTE]
> System.Math 有几种方法使用相同的名称，但区分通过其参数的类型。

键入以下命令以列表**System.Math**类的方法。

```
PS> [System.Math] | Get-Member -Static -MemberType Methods

   TypeName: System.Math

Name            MemberType Definition
----            ---------- ----------
Abs             Method     static System.Single Abs(Single value), static Sy...
Acos            Method     static System.Double Acos(Double d)
Asin            Method     static System.Double Asin(Double d)
Atan            Method     static System.Double Atan(Double d)
Atan2           Method     static System.Double Atan2(Double y, Double x)
BigMul          Method     static System.Int64 BigMul(Int32 a, Int32 b)
Ceiling         Method     static System.Double Ceiling(Double a), static Sy...
Cos             Method     static System.Double Cos(Double d)
Cosh            Method     static System.Double Cosh(Double value)
DivRem          Method     static System.Int32 DivRem(Int32 a, Int32 b, Int3...
Equals          Method     static System.Boolean Equals(Object objA, Object ...
Exp             Method     static System.Double Exp(Double d)
Floor           Method     static System.Double Floor(Double d), static Syst...
IEEERemainder   Method     static System.Double IEEERemainder(Double x, Doub...
Log             Method     static System.Double Log(Double d), static System...
Log10           Method     static System.Double Log10(Double d)
Max             Method     static System.SByte Max(SByte val1, SByte val2), ...
Min             Method     static System.SByte Min(SByte val1, SByte val2), ...
Pow             Method     static System.Double Pow(Double x, Double y)
ReferenceEquals Method     static System.Boolean ReferenceEquals(Object objA...
Round           Method     static System.Double Round(Double a), static Syst...
Sign            Method     static System.Int32 Sign(SByte value), static Sys...
Sin             Method     static System.Double Sin(Double a)
Sinh            Method     static System.Double Sinh(Double value)
Sqrt            Method     static System.Double Sqrt(Double d)
Tan             Method     static System.Double Tan(Double a)
Tanh            Method     static System.Double Tanh(Double value)
Truncate        Method     static System.Decimal Truncate(Decimal d), static...
```

这将显示以下几种数学方法。 下面是演示一些常见的方法是如何工作的命令的列表︰

```
PS> [System.Math]::Sqrt(9)
3
PS> [System.Math]::Pow(2,3)
8
PS> [System.Math]::Floor(3.3)
3
PS> [System.Math]::Floor(-3.3)
-4
PS> [System.Math]::Ceiling(3.3)
4
PS> [System.Math]::Ceiling(-3.3)
-3
PS> [System.Math]::Max(2,7)
7
PS> [System.Math]::Min(2,7)
2
PS> [System.Math]::Truncate(9.3)
9
PS> [System.Math]::Truncate(-9.3)
-9
```

