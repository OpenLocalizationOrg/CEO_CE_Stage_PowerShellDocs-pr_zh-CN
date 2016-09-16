# 导入 DscResource 关键字支持-ModuleVersion 参数

我们已添加到新的参数`Import-DscResource`动态关键字创作 DSC 配置时可用。 配置作者现在可以指定完全模块要加载的版本的 DSC 资源。 关键字的新语法如下︰

```powershell
Import-DscResource [-Name <ResourceName(s)>] [-ModuleName <ModuleName(s)>] [-ModuleVersion <ModuleVersion>]
```

* **名称**︰ 导入的一个或多个 reosurces 名称。
* **ModuleName**︰ 模块名称或 ModuleSpecification 对象的一个或多个要导入的模块。
* **ModuleVersion**︰ 模块 ot 导入的版本。 如果使用，则 ModuleName 必须按名称表示只有一个模块。 

在 Windows PowerShell ISE，它显示使用智能感知的︰

![](../images/Import-DscResource-Modversion.jpg)

**注意**︰`–ModuleVersion`仅可以结合使用参数`–ModuleName`参数。 不能使用仅使用的资源名称`–Name`参数。

之前，若要指定模块版本时加载 DSC 资源的唯一方法是使用模块规范对象，例如︰ `–ModuleName @{ModuleName="UserConfigProvider";ModuleVersion="3.0"}`

