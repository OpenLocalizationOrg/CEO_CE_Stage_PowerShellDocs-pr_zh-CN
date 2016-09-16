# 允许在配置相同重复的资源

DSC 不允许或处理冲突资源定义配置内。 而不是尝试解决冲突，则只会失败。 配置重复使用变得更利用通过复合资源，将更频繁地发生等冲突。 当冲突资源定义相同，DSC 应智能并允许此操作。 此版本中，我们支持多个资源实例中具有相同的定义︰

```powershell
Configuration IIS_FrontEnd
{
    WindowsFeature FE_IIS         #Identical resource
    {
        Ensure = 'Present'
        Name = 'Web-Server'
    }

    WindowsFeature FTP
    {
        Ensure = 'Present'
        Name = 'Web-FTP-Server'
    }
}

Configuration IIS_Worker
{
    WindowsFeature Worker_IIS      #Identical resource
    {
        Ensure = 'Present'
        Name = 'Web-Server'
    }

    WindowsFeature ASP
    {
        Ensure = 'Present'
        Name = 'Web-ASP-Net45'
    }
}

Configuration WebApplication
{
    IIS_Frontend Web {}

    IIS_Worker ASP {}
}
```

在早期版本中，则结果将安装失败的编译由于 WindowsFeature FE_IIS 和 WindowsFeature Worker_IIS 尝试确保 Web 服务器角色的实例之间的冲突。 请注意，*所有*的正在配置的属性是以下两种配置相同。 由于*所有*这两个资源的属性的是相同的这将导致成功编译现在。 

如果两个资源不同的任何属性，它们不会被视为相同，并且编译将失败︰

```powershell
Configuration IIS_FrontEnd
{
    WindowsFeature FE_IIS
    {
        Ensure = 'Present'     # Ensure is Present here
        Name = 'Web-Server'
    }

    WindowsFeature FTP
    {
        Ensure = 'Present'
        Name = 'Web-FTP-Server'
    }
}

Configuration IIS_Worker
{
    WindowsFeature Worker_IIS
    {
        Ensure = 'Absent'      # Ensure property is Absent instead of Present
        Name = 'Web-Server'
    }

    WindowsFeature ASP
    {
        Ensure = 'Present'
        Name = 'Web-ASP-Net45'
    }
}

Configuration WebApplication
{
    IIS_Frontend Web {}

    IIS_Worker ASP {}
}
```

此非常类似配置将失败，因为 WindowsFeature FE_IIS 和 WindowsFeature Worker_IIS 资源不再相同，因此冲突。