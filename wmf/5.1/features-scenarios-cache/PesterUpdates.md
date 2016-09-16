---
标题︰ Pester 更新到版本 3.4.0 作者︰ jaimeo 参与者︰ jkeithb 参与者︰ 李小明 Bankston （专家是 Jim Truher）
---

在 5.1 版本中，使用 PowerShell Pester 附带的版本已更新从 3.3.5 到 3.4.0，添加了提交 https://github.com/pester/Pester/pull/484/commits/3854ae8a1f215b39697ac6c2607baf42257b102e，这样在 Nano Pester 更好的行为。 


您可以通过检查 ChangeLog.md 文件在查看版本 3.3.5 到 3.4.0 中的更改︰ https://github.com/pester/Pester/blob/master/CHANGELOG.md

**已知问题**在 Nano pester 
* 测试针对 Pester 本身仍结果在运行一些故障由于完整 CLR 和核心 CLR 之间的差异，具体地说验证方法不可用的 XmlDocument 类型。 有 6 测试其尝试验证失败的 nunit 输出日志的架构。 
* 一个代码报道测试 curently 失败，因为 Nano 上不存在*WindowsFeature* DSC 资源。 这些故障在通常性能良好。