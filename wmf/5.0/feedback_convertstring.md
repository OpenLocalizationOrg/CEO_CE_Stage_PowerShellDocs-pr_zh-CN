# 转换字符串
**转换字符串**公开"幻通过将替换"功能。 之前和之后的方式来看的文本和**转换字符串**格式示例文本自动提供。 下面是演示-执行人的名字和姓氏，并将其替换为其姓氏、 逗号、 姓氏，并使用句点的首字母。 试一试使用正则表达式，并查看您需要多长。

```powershell
"Lee Holmes", "Steve Lee", "Jeffrey Snover" | Convert-String -Example "Bill Gates=Gates, B.","John Smith=Smith, J."

Holmes, L.
Lee, S.
Snover, J.
```
