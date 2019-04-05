---
title: 引用和 Imports 语句 (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- assemblies [Visual Basic], namespaces
- references [Visual Basic], assembly
- namespaces [Visual Basic], assemblies
- referencing assemblies
- Imports statement [Visual Basic], referencing assemblies
- assemblies [Visual Basic], references
ms.assetid: 38149bd4-0a6f-4b31-b5f8-94a8c33f1600
ms.openlocfilehash: f3396eb3e758dc456d86de80246de24349680f2e
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56973036"
---
# <a name="references-and-the-imports-statement-visual-basic"></a>引用和 Imports 语句 (Visual Basic)
您可以向外部对象提供你的项目通过选择**添加引用**命令**项目**菜单。 在 Visual Basic 中的引用可以指向程序集，与类似类型库但包含的详细信息。  
  
## <a name="the-imports-statement"></a>Imports 语句  
 程序集包含一个或多个命名空间。 当添加对程序集的引用时，还可以添加`Imports`控制该程序集的命名空间的模块中的可见性的模块的语句。 `Imports`语句提供了使您可以使用仅需提供的唯一引用的命名空间一部分的作用域上下文。  
  
 `Imports`语句具有以下语法：  
  
 `Imports [Aliasname =] Namespace`  
  
 `Aliasname` 为短名称，可以使用代码中引用的导入的命名空间的引用。 `Namespace` 是通过在项目中，定义或通过以前的项目引用的命名空间通过提供`Imports`语句。  
  
 模块可以包含任意数量的`Imports`语句。 它们必须出现在任何之后`Option`语句，如果存在，但在之前的任何其他代码。  
  
> [!NOTE]
>  不要混淆与项目引用`Imports`语句或`Declare`语句。 项目引用使得外部对象，例如，在程序集中，对象可用于 Visual Basic 项目。 `Imports`语句用于简化对项目引用的访问，但不提供对这些对象的访问。 `Declare`语句用于声明对外部过程中动态链接库 (DLL) 的引用。  
  
## <a name="using-aliases-with-the-imports-statement"></a>通过导入语句使用别名  
 `Imports`语句，从而更便于访问的类的方法，无需显式类型引用的完全限定的名称。 别名，可将更友好的名称分配到一个命名空间的一部分。 例如，回车/换行序列会导致单个多行上显示的文本是一部分<xref:Microsoft.VisualBasic.ControlChars>中的模块<xref:Microsoft.VisualBasic?displayProperty=nameWithType>命名空间。 若要在不带别名程序中使用此常量，你需要键入以下代码：  
  
 [!code-vb[VbVbalrApplication#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrApplication/VB/Class1.vb#3)]  
  
 `Imports` 语句必须始终为第一个行紧跟任何`Option`模块中的语句。 以下代码片段演示如何导入和分配的别名<xref:Microsoft.VisualBasic.ControlChars?displayProperty=nameWithType>模块：  
  
 [!code-vb[VbVbalrApplication#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrApplication/VB/Class1.vb#4)]  
  
 将来对此命名空间的引用可以是简短得多：  
  
 [!code-vb[VbVbalrApplication#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrApplication/VB/Class1.vb#5)]  
  
 如果`Imports`语句不包括别名名称，而无需限定的模块中可以使用导入的命名空间中定义的元素。 如果指定的别名名称，则它必须用作限定符的名称包含在该命名空间内。  
  
## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualBasic.ControlChars>
- <xref:Microsoft.VisualBasic>
- [在 Visual Basic 中的命名空间](../../../visual-basic/programming-guide/program-structure/namespaces.md)
- [.NET 中的程序集](../../../standard/assembly/index.md)
- [如何：使用命令行创建和使用程序集](../../../visual-basic/programming-guide/concepts/assemblies-gac/how-to-create-and-use-assemblies-using-the-command-line.md)
- [Imports 语句（.NET 命名空间和类型）](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)
