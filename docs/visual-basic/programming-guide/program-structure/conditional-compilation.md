---
title: Visual Basic 中的条件编译
ms.date: 07/20/2015
helpviewer_keywords:
- conditional compilation [Visual Basic], about conditional compilation
- compilation [Visual Basic], conditional
ms.assetid: 9c35e55e-7eee-44fb-a586-dad1f1884848
ms.openlocfilehash: 828edf2e5491394f5ac802b5c9babfb3df359e59
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56967841"
---
# <a name="conditional-compilation-in-visual-basic"></a>Visual Basic 中的条件编译
在中*条件编译*，而其他人将被忽略，将有选择地编译特定程序中的代码块。  
  
 例如，你可能想要编写调试语句来比较不同的方法的速度到相同的编程任务，也可能想要本地化为多种语言的应用程序。 条件编译语句被设计为在编译时，不是在运行时期间运行。  
  
 表示用于使用有条件地编译的代码块`#If...Then...#Else`指令。 例如，若要创建法语和德语版本的相同应用程序的同一源代码，嵌入中特定于平台的代码段`#If...Then`使用的预定义的常量的语句`FrenchVersion`和`GermanVersion`。 下面的示例演示如何：  
  
 [!code-vb[VbVbalrConditionalComp#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConditionalComp/VB/Class1.vb#5)]  
  
 如果设置的值`FrenchVersion`条件编译常量为`True`在编译时，法语版的条件代码进行编译。 如果设置的值`GermanVersion`常量到`True`，编译器将使用德语版本。 如果未设置`True`，在最后一个代码`Else`块将运行。  
  
> [!NOTE]
>  自动完成功能将不函数时编辑代码，并使用条件编译指令，如果代码不是当前分支的一部分。  
  
## <a name="declaring-conditional-compilation-constants"></a>声明条件编译常量  
 可以通过三种方式之一来设置条件编译常量：  
  
-   在**项目设计器**  
  
-   在命令行使用命令行编译器时  
  
-   在代码中  
  
 条件编译常量具有特殊的作用域，并且不能从标准的代码访问。 条件编译常数的范围是依赖于它的设置的方式。 下表列出了使用上面提到的三种方法的每个声明的常量的作用域。  
  
|如何设置常量|常量的作用域|  
|---|---|  
|**项目设计器**|在项目中的所有文件是公共的|  
|命令行|传递到命令行编译器的所有文件是公共的|  
|`#Const` 在代码中的语句|专用于在其中声明的文件|  
  
|若要在项目设计器中设置常量|  
|---|  
|-之前创建可执行文件，在中设置常量**项目设计器**中提供的步骤[管理项目和解决方案属性](/visualstudio/ide/managing-project-and-solution-properties)。|  
  
|在命令行上设置常量|  
|---|  
|-使用 **/d**开关输入条件编译常量，如以下示例所示：<br />     `vbc MyProj.vb /d:conFrenchVersion=–1:conANSI=0`<br />     不所需之间的任何空间 **/d**开关与第一个常数。 有关详细信息，请参阅[/define (Visual Basic)](../../../visual-basic/reference/command-line-compiler/define.md)。<br />     命令行声明会覆盖输入声明**项目设计器**，但不是清除它们。 参数中设置**项目设计器**始终有效，对于后续编译。<br />     时编写代码本身中的常量，没有严格的规则对其位置，因为它们的作用域是整个模块声明它们。|  
  
|若要在代码中设置常量|  
|---|  
|-将常量放在声明块中使用它们的模块。 这有助于保持代码组织有序且易于阅读。|  
  
## <a name="related-topics"></a>相关主题  
  
|标题|描述|  
|---|---|  
|[程序结构和代码约定](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)|提供有关使代码易于阅读和维护建议。|  
  
## <a name="reference"></a>参考  
 [#Const 指令](../../../visual-basic/language-reference/directives/const-directive.md)  
  
 [#If...Then...#Else 指令](../../../visual-basic/language-reference/directives/if-then-else-directives.md)  
  
 [/define (Visual Basic)](../../../visual-basic/reference/command-line-compiler/define.md)
