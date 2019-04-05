---
title: 如何：从 Visual Basic 引用 COM 对象
ms.date: 07/20/2015
helpviewer_keywords:
- COM interop [Visual Basic], referencing COM objects
- referencing objects, COM objects from Visual Basic
- objects [Visual Basic], referencing
- COM objects, referencing
- interop assemblies
ms.assetid: 9c518fb4-27d9-4112-9e6a-5a7d0210af6f
ms.openlocfilehash: 9e88f5f093ce55d3d80da9b38689016872ea12cb
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56980186"
---
# <a name="how-to-reference-com-objects-from-visual-basic"></a>如何：从 Visual Basic 引用 COM 对象
在 Visual Basic 中，添加对包含类型库的 COM 对象的引用需要互操作程序集创建为 COM 库。 对 COM 对象的成员的引用是路由到互操作程序集，并转发给实际的 COM 对象。 从 COM 对象的响应路由到互操作程序集，并将其转发到你[!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)]应用程序。  
  
 无需通过将 COM 对象的类型信息嵌入在.NET 程序集中使用互操作程序集，即可引用 COM 对象。 若要嵌入类型信息，请设置`Embed Interop Types`属性设置为`True`对 COM 对象的引用。 如果你使用命令行编译器进行编译，请使用`/link`选项来引用 COM 库。 有关详细信息，请参阅[/link (Visual Basic)](../../../visual-basic/reference/command-line-compiler/link.md)。  
  
 添加对类型库中的集成的开发环境 (IDE) 的引用时，Visual Basic 会自动创建互操作程序集。 在从命令行处理时，可以使用 Tlbimp 实用工具来手动创建互操作程序集。  
  
### <a name="to-add-references-to-com-objects"></a>若要添加对 COM 对象的引用  
  
1.  上**项目**菜单中，选择**添加引用**，然后单击**COM**对话框中的选项卡。  
  
2.  选择你想要从 COM 对象的列表中使用的组件。  
  
3.  若要简化对互操作程序集的访问，将添加`Imports`到顶部的类或模块将在其中使用 COM 对象的语句。 例如，下面的代码示例将导入命名空间`INKEDLib`中所引用的对象`Microsoft InkEdit Control 1.0`库。  
  
     [!code-vb[VbVbalrInterop#40](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#40)]  
  
### <a name="to-create-an-interop-assembly-using-tlbimp"></a>若要创建使用 Tlbimp 的互操作程序集  
  
1.  将 Tlbimp 的位置添加到搜索路径中，如果它已不是搜索路径的一部分，并且您目前不所在的目录。  
  
2.  调用 Tlbimp 从命令提示符下，提供以下信息：  
  
    -   包含类型库的 DLL 的名称和位置  
  
    -   名称和命名空间的位置信息应放置的位置  
  
    -   目标互操作程序集的名称和位置  
  
     以下代码提供了一个示例：  
  
    ```  
    Tlbimp test3.dll /out:NameSpace1 /out:Interop1.dll  
    ```  
  
     可以使用 Tlbimp 来创建互操作程序集的类型库，甚至对于未注册的 COM 对象。 但是，由互操作程序集引用的 COM 对象必须正确注册它们将被用于在计算机上。 可以使用随 Windows 操作系统附带的 Regsvr32 实用工具来注册 COM 对象。  
  
## <a name="see-also"></a>请参阅

- [COM 互操作](../../../visual-basic/programming-guide/com-interop/index.md)
- [Tlbimp.exe（类型库导入程序）](../../../framework/tools/tlbimp-exe-type-library-importer.md)
- [Tlbexp.exe（类型库导出程序）](../../../framework/tools/tlbexp-exe-type-library-exporter.md)
- [演练：使用 COM 对象实现继承](../../../visual-basic/programming-guide/com-interop/walkthrough-implementing-inheritance-with-com-objects.md)
- [互操作性疑难解答](../../../visual-basic/programming-guide/com-interop/troubleshooting-interoperability.md)
- [Imports 语句（.NET 命名空间和类型）](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)
