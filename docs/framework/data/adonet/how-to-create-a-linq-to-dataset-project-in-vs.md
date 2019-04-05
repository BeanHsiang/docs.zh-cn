---
title: 创建 LINQ to DataSet 项目在 Visual Studio 中
ms.date: 08/15/2018
ms.assetid: 49ba6cb0-cdd2-4571-aeaa-25bf0f40e9b3
ms.openlocfilehash: 22763d3b9581d09d7bdda0c09480f8d36bb8e2ec
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53154029"
---
# <a name="how-to-create-a-linq-to-dataset-project-in-visual-studio"></a>如何：创建 LINQ to DataSet 项目在 Visual Studio 中

不同类型的 LINQ 项目需要某些程序集引用和导入命名空间 (Visual Basic) 或[使用](../../../csharp/language-reference/keywords/using-directive.md)指令 (C#)。 LINQ 的最低要求是对的引用*System.Core.dll*和一个`using`指令<xref:System.Linq>。

这些要求被提供默认情况下，如果在 Visual Studio 2017 中创建新 C# 控制台应用项目。 如果您要从 Visual Studio 的早期版本升级项目，您可能必须手动提供这些与 LINQ 相关的引用。

LINQ 到数据集需要两个其他引用*System.Data.dll*并*System.Data.DataSetExtensions.dll*。

> [!NOTE]
> 如果您正在构建的命令提示符下，则必须手动引用中与 LINQ 相关的 Dll *%ProgramFiles%\Reference Assemblies\Microsoft\Framework\v3.5*。

## <a name="to-enable-linq-to-dataset-functionality"></a>启用 LINQ to DataSet 功能

请按照下列步骤以启用 LINQ to DataSet 中的现有项目的功能。

1. 将引用添加到**System.Core**， **System.Data**，并**System.Data.DataSetExtensions**。

   在中**解决方案资源管理器**，右键单击**引用**节点，然后选择**添加引用**。 在中**引用管理器**对话框中，选择**System.Core**， **System.Data**，以及**System.Data.DataSetExtensions**。 选择“确定”。

1. 添加[使用](../../../csharp/language-reference/keywords/using-directive.md)指令 (或[Imports 语句](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)在 Visual Basic 中) 的**System.Data**并**System.Linq**。

   ```csharp
   using System.Data;
   using System.Linq;
   ```

1. （可选） 添加`using`指令 (或`Imports`语句) 的**System.Data.Common**或**System.Data.SqlClient**，取决于如何连接到数据库。

## <a name="see-also"></a>请参阅

- [开始使用 LINQ to DataSet](../../../../docs/framework/data/adonet/getting-started-linq-to-dataset.md)
