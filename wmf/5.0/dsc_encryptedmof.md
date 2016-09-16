# 默认情况下加密 MOF 文档

配置文档包含敏感信息。 在早期版本的 DSC 您需要分发和安全配置内的凭据才能管理证书。 对于许多，这是重大管理负担以及了即使使用的所有工作目的您仍然保持的一些配置信息未，而且不会受保护的。 

因为不再是这样**Mof 受默认的所有配置**。 需要没有证书或元配置设置。 任何时候，配置 MOF 保存到磁盘通过本地配置管理器 (LCM) 上的目标节点，它加密。 Mof 使用[DPAPI](https://msdn.microsoft.com/en-us/library/ms995355.aspx)进行加密。 **注意︰**配置脚本生成的 Mof 未加密。

**示例︰**推送模式中的加密![MOF 加密](../images/MOF_Encryption.jpg)

如果您已经使用密码加密证书方法或者需要额外的安全密码，[基于加密的证书的现有方法](https://msdn.microsoft.com/en-us/powershell/dsc/securemof)将继续工作。 结果将使用 DPAPIs 完全加密 MOF 文档并此外使用密码加密内它。

此加密仅适用于配置 MOF 文档 （pending.mof、 current.mof、 previous.mof 和部分 Mof 的）。 以纯文本仍保存元配置 Mof，因为它们不太可能包含机密信息。
