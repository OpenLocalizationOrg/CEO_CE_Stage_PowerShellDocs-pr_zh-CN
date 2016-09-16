# 有关准备发布操作过程模块相关性的逻辑
1.  列出作为 RequiredModules 的一部分的模块被视为相关性。
2.  作为 NestedModules，其模块基不是在指定的模块基下，列出的模块被视为依赖项。

3.  相关性上方程序应该能在同一个目标存储库，否则发布操作会导致错误。
    例如︰ 如果在存储库 SnippetPx' 不可用，下面错误将会引发。
    ```powershell
    Publish-PSArtifactUtility : PowerShellGet cannot resolve the module dependency 'SnippetPx' of the module 'TypePx' on the repository 'LocalRepo'. Verify that the dependent module 'SnippetPx' is available in the repository 'LocalRepo'. If this dependent
    'SnippetPx' is managed externally, add it to the ExternalModuleDependencies entry in the PSData section of the module manifest.
    ```
4.  某些模块依赖关系可外部管理，这种情况下应将它们添加到模块清单的 PSData 部分中的 ExternalModuleDependencies 条目。
    在上面的错误消息部件下方
    ```powershell
    If this dependent 'SnippetPx' is managed externally, add it to the ExternalModuleDependencies entry in the PSData section of the module manifest.
    ```

*模块安装期间，上面准备依赖项列表用于安装依赖项。*

*请确保您的模块相关性 $env 下可用︰ 在您的系统期间 PSModulePath 发布操作。*
