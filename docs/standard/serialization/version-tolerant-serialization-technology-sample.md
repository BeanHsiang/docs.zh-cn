---
title: 版本容错序列化技术示例
ms.date: 03/30/2017
ms.assetid: 2a183664-bfbf-4ff0-96f6-c836284ea916
ms.openlocfilehash: b874a347924f6d15e2e6164092b819321384ca3f
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54681113"
---
# <a name="version-tolerant-serialization-technology-sample"></a>版本容错序列化技术示例
[下载示例](https://download.microsoft.com/download/4/7/B/47B2164C-E780-4B10-8DE4-2CB5B886E0A6/Technologies/Serialization/Runtime%20Serialization/VTS.zip.exe)  
  
 此示例演示 .NET 序列化的版本容错功能。 此示例生成的应用程序使用不同版本的 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 对数据进行序列化和反序列化。 尽管存在不同类型的版本，但应用程序仍可以进行无缝通信。 有关详细信息，请参阅[版本容错序列化](../../../docs/standard/serialization/version-tolerant-serialization.md)。  
  
### <a name="to-build-the-sample-using-the-command-prompt"></a>使用命令提示生成示例  
  
1.  打开命令提示窗口，然后定位到该示例的语言特定子目录（在 V1 Application 或 V2 Application 之下）之一。  
  
2.  在命令行中键入“msbuild.exe \<ver> application.sln”（其中 \<ver> 为 v1 或 v2）。  
  
### <a name="to-build-the-sample-using-visual-studio"></a>使用 Visual Studio 生成示例  
  
1.  打开[!INCLUDE[fileExplorer](../../../includes/fileexplorer-md.md)]，定位到该示例的特定语言的子目录。  
  
2.  定位到您在上一步中选择的目录的 V1 Application 子目录。  
  
3.  双击 V1 Application.sln 的图标，以便在 Visual Studio 中打开该文件。  
  
4.  在 **“生成”** 菜单上，单击 **“生成解决方案”**。  
  
5.  定位到 V2 Application 子目录，重复前面两个步骤，以生成 V2 Application。  
  
 应用程序将在其各自项目目录的默认 \bin 或 \bin\Debug 子目录中生成。  
  
### <a name="to-run-the-sample"></a>运行示例  
  
1.  在命令提示窗口中，定位到您在生成示例应用程序时选择的语言特定的子目录。  
  
2.  在命令行中键入“runme.cmd”，以同时运行这两个应用程序。  
  
 或者，定位到包含新的可执行文件的目录，然后按顺序运行这些文件。  
  
> [!NOTE]
>  此示例生成控制台应用程序。 必须在命令提示窗口中启动并运行这些应用程序，才能查看相应的输出。  
  
## <a name="see-also"></a>请参阅

- <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>
- <xref:System.IO.FileStream>
