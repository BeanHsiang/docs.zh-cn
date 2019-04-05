---
title: 名称“<name>”未声明
ms.date: 10/10/2018
f1_keywords:
- bc30451
- vbc30451
helpviewer_keywords:
- BC30451
ms.assetid: 765f099b-e21e-47c6-a906-a065444e56b3
ms.openlocfilehash: 3aadc49f91021409123550ba2712f1acf5b99d83
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55260121"
---
# <a name="name-name-is-not-declared"></a>名称\<名称 > 未声明
语句引用的编程元素，但编译器找不到具有相同名称的元素。  
  
 **错误 ID:** BC30451  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
1. 检查引用语句中名称的拼写。 Visual Basic 是不区分大小写，但拼写中的任何其他变体都会被视为完全不同的名称。 请注意，下划线 (`_`) 是名称的一部分，因此也是拼写的一部分。  
  
2. 检查你是否拥有成员访问运算符 (`.`) 对象及其成员之间。 例如，如果你拥有名为 <xref:System.Windows.Forms.TextBox> 的 `TextBox1`控件，则要键入 <xref:System.Windows.Forms.TextBoxBase.Text%2A> 才可访问其 `TextBox1.Text`。 如果你转而键入 `TextBox1Text`，则会创建不同的名称。  
  
3. 如果任何对象成员访问语法正确的拼写正确，验证已声明元素。 有关详细信息，请参阅[Declared Elements](../../programming-guide/language-features/declared-elements/index.md)。  
  
4. 如果已声明的编程元素，检查它是否在作用域中。 如果引用语句位于声明编程元素的区域外，您可能需要限定元素名称。 有关详细信息，请参阅 [Scope in Visual Basic](../../programming-guide/language-features/declared-elements/scope.md)。  

5. 如果不使用完全限定的类型和成员名称 (例如，你的代码是指属性作为`MethodInfo.Name`而不是`System.Reflection.MethodInfo.Name`)，添加[Imports 语句](../statements/imports-statement-net-namespace-and-type.md)。

6. 如果您尝试编译 SDK 样式项目 (具有的项目\*.vbproj 文件以在行开头`<Project Sdk="Microsoft.NET.Sdk">`)，和错误消息引用的类型或成员中的 Microsoft.VisualBasic.dll 程序集，来配置应用程序使用 Visual Basic 运行库的引用进行编译。 默认情况下，库的一个子集嵌入在程序集 SDK 样式项目中。

   例如，下面的示例无法进行编译，因为<xref:Microsoft.VisualBasic.CompilerServices.Conversions.ToInteger%2A?displayProperty=fullName>找不到方法。 它不嵌入在你的应用程序中包含的 Visual Basic 运行时的子集。  

   [!code-vb[BC30451](~/samples/snippets/visualbasic/language-reference/error-messages/bc30451/program1.vb)]

   若要解决此错误，将添加`<VBRuntime>Default</VBRuntime>`的项目元素`<PropertyGroup>`部分中，如下面的 Visual Basic 项目文件所示。

   [!code-vb[BC30451](~/samples/snippets/visualbasic/language-reference/error-messages/bc30451/vbruntime.vbproj?highlight=6)]

## <a name="see-also"></a>请参阅

- [声明和常量摘要](../../../visual-basic/language-reference/keywords/declarations-and-constants-summary.md)
- [Visual Basic 命名约定](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)
- [已声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)
- [对已声明元素的引用](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
