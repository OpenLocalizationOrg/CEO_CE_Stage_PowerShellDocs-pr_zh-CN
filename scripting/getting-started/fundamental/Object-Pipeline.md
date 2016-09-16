---
title: "对象渠道"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 523d8ae4-d743-47a4-b79a-806130ca688a
ms.openlocfilehash: 570805d6ceb4613f0efc8095f08ce79d90514f62
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 对象渠道
管线像一系列的管道连接段。 通过每个段传递沿管线移动的项目。 若要创建管线 Windows PowerShell，您可以连接与管道运算符命令"|"。 每个命令的输出用作输入到下一步命令。

管线可以说是使用命令行界面中的最有价值概念。 使用正确管线不仅可以减少工作所涉及的输入复杂的命令，但还使其更易于查看的命令中的工作流。 管线相关有用特征是，单独运行每个项目，因为您没有修改它们基于是否将管道中有零、 一个或多个项目。 此外，管道 （称为管线元素） 中的每个命令通常将其输出传递给渠道--项目中的下一个命令。 这通常减少复杂的命令的资源需求，并使您可以开始立即获取输出。

这一章，我们将介绍如何与 Windows PowerShell 渠道不同的最常用的外壳的管道，并且然后演示以帮助控制管道输出以及查看渠道的运行方式，您可以使用一些基本工具。

