---
title: 无法发出程序集：<error message>
ms.date: 08/14/2018
f1_keywords:
- vbc30145
- bc30145
helpviewer_keywords:
- BC30145
ms.assetid: 2e7eb2b9-eda6-4bdb-95cc-72c7f0be7528
ms.openlocfilehash: d564f4f4462a691504297d65575956c5f06691ca
ms.sourcegitcommit: 01ea420eaa4bf76d5fc47673294c8881379b3369
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/06/2019
ms.locfileid: "55759218"
---
# <a name="unable-to-emit-assembly-error-message"></a>无法发出程序集：\<错误消息 >

Visual Basic 编译器调用程序集链接器 (*Al.exe*，也称为 Alink) 生成的程序集具有一个清单和链接器可创建程序集的发出阶段报告错误。

**错误 ID:** BC30145

## <a name="to-correct-this-error"></a>更正此错误

1. 检查引用的错误信息并参考主题[Al.exe](../../../framework/tools/al-exe-assembly-linker.md)以获得进一步的解释和建议。

2. 请尝试使用手动签名程序集[Al.exe](../../../framework/tools/al-exe-assembly-linker.md)或[Sn.exe （强名称工具）](../../../framework/tools/sn-exe-strong-name-tool.md)。

3. 如果仍然出现错误，则收集有关该情况的信息并通知 Microsoft 产品支持服务。

### <a name="to-sign-the-assembly-manually"></a>手动对程序集进行签名

1. 使用[Sn.exe （强名称工具）](../../../framework/tools/sn-exe-strong-name-tool.md)) 创建公钥/私钥对文件。

   此文件具有 *.snk*扩展。

2. 从项目中删除生成错误的 COM 引用。

3. 打开[Visual Studio 的开发人员命令提示](../../../framework/tools/developer-command-prompt-for-vs.md)。

   在 Windows 10 中，输入**开发人员命令提示**任务栏上的搜索框。 然后，选择**VS 2017 开发人员命令提示**从结果列表中。

4. 将目录更改为你想要放置程序集包装的目录。

5. 输入以下命令：

    ```cmd
    tlbimp <path to COM reference file> /out:<output assembly name> /keyfile:<path to .snk file>
    ```

   可能输入的实际命令的一个示例是：

    ```cmd
    tlbimp c:\windows\system32\msi.dll /out:Interop.WindowsInstaller.dll /keyfile:"c:\documents and settings\mykey.snk"
    ```

   > [!TIP]
   > 如果路径或文件名包含空格，请使用双引号引起来。

6. 在 Visual Studio 中，添加对刚创建的文件的.NET 程序集引用。

## <a name="see-also"></a>请参阅

- [Al.exe](../../../framework/tools/al-exe-assembly-linker.md)
- [Sn.exe（强名称工具）](../../../framework/tools/sn-exe-strong-name-tool.md)
- [如何：创建公钥/私钥对](../../../framework/app-domains/how-to-create-a-public-private-key-pair.md)
- [与我们交流](/visualstudio/ide/talk-to-us)