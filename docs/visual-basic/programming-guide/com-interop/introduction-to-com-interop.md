---
title: COM 互操作介绍 (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- interop assemblies
- COM interop [Visual Basic], about COM interop
ms.assetid: 8bd62e68-383d-407f-998b-29aa0ce0fd67
ms.openlocfilehash: e4421cbc40cdccc1dbbaeb459cb12fda0ee407cf
ms.sourcegitcommit: 8f95d3a37e591963ebbb9af6e90686fd5f3b8707
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2019
ms.locfileid: "56745594"
---
# <a name="introduction-to-com-interop-visual-basic"></a>COM 互操作介绍 (Visual Basic)
组件对象模型 (COM) 允许到其他组件和主机应用程序公开其功能的对象。 虽然 COM 对象的基础 Windows 编程的许多年来，应用程序面向公共语言运行时 (CLR) 提供了许多优点。  
  
 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] com 开发的那些，最终将取代应用程序 到那时，您可能需要使用或通过使用 Visual Studio 创建 COM 对象。 通过 COM 互操作性或*COM 互操作*，使您能够使用现有的 COM 对象，同时转换到[!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)]您自己的节奏。  
  
 通过使用[!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)]若要创建 COM 组件，可以使用免注册 COM 互操作。 这样可以控制多个版本的计算机上，安装并可让最终用户使用 XCOPY 或 FTP 复制到其计算机上的相应目录的应用程序可以运行时启用哪些 DLL 版本。 有关详细信息，请参阅[免注册 COM 互操作](../../../framework/interop/registration-free-com-interop.md)。  
  
## <a name="managed-code-and-data"></a>托管的代码和数据  
 为开发的代码[!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)]被称为*托管代码*，并包含由 CLR 使用元数据。 使用的数据[!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)]应用程序称为*托管数据*因为运行时管理与数据相关的任务，比如分配和回收内存以及执行类型检查。 默认情况下，Visual Basic.NET 中使用托管的代码和数据，但您可以访问的非托管的代码和 COM 对象使用互操作程序集 （稍后介绍在此页上） 的数据。  
  
## <a name="assemblies"></a>程序集  
 程序集是主要构建基块[!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)]应用程序。 它是功能的一个已生成、 版本控制，并作为单个实现单元包含一个或多个文件已部署的集合。 每个程序集包含程序集清单。  
  
## <a name="type-libraries-and-assembly-manifests"></a>类型库和程序集清单  
 类型库描述 COM 对象，如成员名称和数据类型的特征。 程序集清单执行的相同函数[!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)]应用程序。 它们包括有关以下信息：  
  
-   程序集标识、 版本、 区域性和数字签名。  
  
-   组成程序集实现的文件。  
  
-   类型和构成该程序集的资源。 这包括那些从其导出。  
  
-   对其他程序集的编译时依赖项。  
  
-   要正确运行的程序集所需的权限。  
  
 有关程序集和程序集清单的详细信息，请参阅[.NET 中的程序集](../../../standard/assembly/index.md)。  
  
### <a name="importing-and-exporting-type-libraries"></a>导入和导出类型库  
 Visual Studio 包含一个实用程序，Tlbimp，它允许您从类型库到导入信息[!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)]应用程序。 通过使用 Tlbexp 实用工具，可以从程序集生成类型库。  
  
 Tlbimp 和 Tlbexp 有关的信息，请参阅[Tlbimp.exe （类型库导入程序）](../../../framework/tools/tlbimp-exe-type-library-importer.md)并[Tlbexp.exe （类型库导出程序）](../../../framework/tools/tlbexp-exe-type-library-exporter.md)。  
  
## <a name="interop-assemblies"></a>互操作程序集  
 互操作程序集都[!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)]程序集的桥之间托管和非托管代码，映射到等效的 COM 对象成员[!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)]管理成员。 创建 Visual Basic.NET 的互操作程序集处理的许多使用 COM 对象，如互操作封送处理的详细信息。  
  
## <a name="interoperability-marshaling"></a>互操作封送处理  
 所有[!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)]应用程序共享一组实现的对象，无论使用的编程语言的互操作性的常见类型。 参数和返回值的 COM 对象有时使用不同于托管代码中使用的数据类型。 *互操作封送处理*随着对象移动到和从 COM 对象是打包参数和返回值为等效的数据类型的过程。 有关详细信息，请参阅[互操作封送处理](../../../framework/interop/interop-marshaling.md)。  
  
## <a name="see-also"></a>请参阅

- [COM 互操作](../../../visual-basic/programming-guide/com-interop/index.md)
- [演练：使用 COM 对象实现继承](../../../visual-basic/programming-guide/com-interop/walkthrough-implementing-inheritance-with-com-objects.md)
- [与非托管代码交互操作](../../../framework/interop/index.md)
- [互操作性疑难解答](../../../visual-basic/programming-guide/com-interop/troubleshooting-interoperability.md)
- [在.NET 中的程序集](../../../standard/assembly/index.md)
- [Tlbimp.exe（类型库导入程序）](../../../framework/tools/tlbimp-exe-type-library-importer.md)
- [Tlbexp.exe（类型库导出程序）](../../../framework/tools/tlbexp-exe-type-library-exporter.md)
- [互操作封送处理](../../../framework/interop/interop-marshaling.md)
- [免注册 COM 互操作](../../../framework/interop/registration-free-com-interop.md)
