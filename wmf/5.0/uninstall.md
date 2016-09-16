# 卸载说明进行操作

## 使用命令提示符
1.  打开**命令提示符。**
2.  运行[Windows 更新独立启动器](https://support.microsoft.com/en-us/kb/934307)，如下所示︰

在 Windows Server 2012 R2 和 Windows 8.1:
```powershell
wusa /uninstall /kb:3134758
```
在 Windows Server 2012:
```powershell
wusa /uninstall /kb:3134759
```
在 Windows Server 2008 R2 SP1 和 Windows 7 SP1:
```powershell
wusa /uninstall /kb:3134760
```

## 使用控制面板
1.  打开**控制面板。**
2.  打开**程序**，然后打开**卸载程序。**
3.  单击**查看已安装的更新。**
4.  从已安装更新的列表中选择**Windows Management Framework 5.0** 。 这对应于*KB3134758*、 *KB3134759*或*KB3134760*。 单击**卸载。**
