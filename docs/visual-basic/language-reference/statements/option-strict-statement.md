---
title: Option Strict 语句 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Strict
- vb.OptionStrict
helpviewer_keywords:
- Strict keyword [Visual Basic]
- Option Strict statement [Visual Basic]
- conversions [Visual Basic], implicit
- late binding [Visual Basic]
- implicit conversions [Visual Basic]
ms.assetid: 5883e0c1-a920-4274-8e46-b0ff047eaee5
ms.openlocfilehash: adfac0eebc0d50ed3c8c523c0442636b05901c18
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57355124"
---
# <a name="option-strict-statement"></a>Option Strict Statement
隐式数据类型将转换限制为仅进行扩大转换，不允许后期绑定，并禁止隐式键入会导致`Object`类型。  
  
## <a name="syntax"></a>语法  
  
```  
Option Strict { On | Off }  
```  
  
## <a name="parts"></a>部件  
  
|术语|定义|  
|---|---|  
|`On`|可选。 使`Option Strict`检查。|  
|`Off`|可选。 禁用`Option Strict`检查。|  
  
## <a name="remarks"></a>备注  
 当`Option Strict On`或`Option Strict`出现在文件中，以下情况会导致编译时错误：  
  
-   隐式收缩转换  
  
-   后期绑定  
  
-   隐式键入会导致 `Object` 类型  
  
> [!NOTE]
>  您可以设置的警告配置[编译页，项目设计器 (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)，有三个设置对应于三个条件会导致编译时错误。 有关如何使用这些设置的信息，请参阅[若要在 IDE 中设置警告配置](../../../visual-basic/language-reference/statements/option-strict-statement.md#conditions)本主题中更高版本。  
  
 `Option Strict Off`语句关闭错误和警告检查所有三个条件，即使关联的 IDE 设置指定要打开这些错误或警告。 `Option Strict On`语句启用错误和警告检查所有三个条件，即使关联的 IDE 设置指定要关闭这些错误或警告。  
  
 如果使用，`Option Strict`语句必须出现在文件中的任何其他源代码语句之前。  
  
 当您将设置`Option Strict`到`On`，Visual Basic 会检查所有编程元素指定数据类型。 可以显式指定，或通过使用局部类型推理来指定数据类型。 建议为所有编程元素指定数据类型，原因如下：  
  
-   这样，对变量和参数的 IntelliSense 支持。 这使您可以键入代码时查看其属性和其他成员。  
  
-   它使编译器能够执行类型检查。 类型检查可帮助您找到可以在运行时因类型转换错误而失败的语句。 它还标识对不支持这些方法的对象上的方法的调用。  
  
-   它可加快执行的代码。 原因之一就是，如果不指定编程元素的数据类型，Visual Basic 编译器为其分配`Object`类型。 已编译的代码可能需要将之间来回转换`Object`和其他数据类型，这会降低性能。  
  
## <a name="implicit-narrowing-conversion-errors"></a>隐式收缩转换错误  
 隐式数据类型转换为收缩转换时，将发生隐式收缩转换错误。  
  
 Visual Basic 可以将多个数据类型转换为其他数据类型。 一种数据类型的值转换为精度较低或容量较小的数据类型时，会发生数据丢失。 如果这种收缩转换失败，会发生运行时错误。 `Option Strict` 可确保在编译时通知这些收缩转换，这样可以避免它们。 有关详细信息，请参阅[隐式转换和显式转换](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)并[Widening and Narrowing Conversions](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)。  
  
 可能会导致错误的转换在表达式中包含发生的隐式转换。 有关详细信息，请参阅下列主题：  
  
-   [+ 运算符](../../../visual-basic/language-reference/operators/addition-operator.md)  
  
-   [+= 运算符](../../../visual-basic/language-reference/operators/addition-assignment-operator.md)  
  
-   [\ 运算符 (Visual Basic)](../../../visual-basic/language-reference/operators/integer-division-operator.md)  
  
-   [/ = 运算符 (Visual Basic)](../../../visual-basic/language-reference/operators/floating-point-division-assignment-operator.md)  
  
-   [Char 数据类型](../../../visual-basic/language-reference/data-types/char-data-type.md)  
  
 当使用连接字符串[& 运算符](../../../visual-basic/language-reference/operators/concatenation-operator.md)，会考虑所有转换为字符串会扩大。 因此这些转换不会生成隐式收缩转换错误，即使`Option Strict`上。  
  
 如果收缩转换时调用的方法有一个具有不同于相应参数的数据类型的参数，导致编译时错误`Option Strict`上。 可以通过使用扩大转换或显式转换来避免编译时错误。  
  
 隐式收缩转换错误会抑制在编译时为中的元素从`For Each…Next`循环控制变量的集合。 发生这种情况即使`Option Strict`上。 有关详细信息，请参阅中的"收缩转换"部分[为每个...下一条语句](../../../visual-basic/language-reference/statements/for-each-next-statement.md)。  
  
## <a name="late-binding-errors"></a>后期绑定错误  
 如果将对象分配给声明为 `Object` 类型的变量，则该对象为晚期绑定。 有关详细信息，请参阅[早期绑定和后期绑定](../../../visual-basic/programming-guide/language-features/early-late-binding/index.md)。  
  
## <a name="implicit-object-type-errors"></a>隐式对象类型错误  
 如果无法为已声明的变量推断出合适的类型，则会发生隐式对象类型错误，因此 `Object` 类型是推断出来的。 这主要是在未使用 `As` 子句的情况下使用 `Dim` 语句声明变量，且 `Option Infer` 为关闭时发生的。 有关详细信息，请参阅[Option Infer 语句](../../../visual-basic/language-reference/statements/option-infer-statement.md)并[Visual Basic 语言规范](../../../visual-basic/reference/language-specification/index.md)。  
  
 方法参数`As`子句是可选的如果`Option Strict`处于关闭状态。 但是，如果任何一个参数使用`As`子句，它们都必须使用它。 如果`Option Strict`处于打开状态，`As`子句是必需的每个参数定义。  
  
 如果不使用声明一个变量`As`子句并将其设置为`Nothing`，该变量的类型为`Object`。 在这种情况下发生任何编译时错误时`Option Strict`位于和`Option Infer`上。 此示例是`Dim something = Nothing`。  
  
### <a name="default-data-types-and-values"></a>默认数据类型和值  
 下表描述了指定的数据类型和初始值设定项中的各种组合的结果[Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)。  
  
|是否指定数据类型？|是否指定初始值设定项？|示例|结果|  
|---|---|---|---|  
|否|否|`Dim qty`|如果 `Option Strict` 处于关闭状态（默认），则将变量设置为 `Nothing`。<br /><br /> 如果 `Option Strict` 处于打开状态，则发生编译时错误。|  
|否|是|`Dim qty = 5`|如果 `Option Infer` 处于打开状态（默认），则变量采用初始值设定项的数据类型。 请参阅[局部类型推理](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)。<br /><br /> 如果 `Option Infer` 和 `Option Strict` 均处于关闭状态，则变量采用 `Object` 的数据类型。<br /><br /> 如果 `Option Infer` 处于关闭状态但 `Option Strict` 处于打开状态，则发生编译时错误。|  
|是|否|`Dim qty As Integer`|将变量初始化为数据类型的默认值。 有关详细信息，请参阅[Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)。|  
|是|是|`Dim qty  As Integer = 5`|如果初始值设定项的数据类型不可转换为指定数据类型，则会发生编译时错误。|  
  
## <a name="when-an-option-strict-statement-is-not-present"></a>Option Strict 语句不存在  
 如果源代码不包含`Option Strict`语句中， **Option strict**上设置[编译页，项目设计器 (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)使用。 **编译页**具有可提供对生成错误的条件的其他控制设置。  
  
 如果使用命令行编译器，则可以使用[/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)编译器选项指定的设置`Option Strict`。  
  
### <a name="to-set-option-strict-in-the-ide"></a>若要在 IDE 中设置 Option Strict  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
1.  在“解决方案资源管理器”中，选择一个项目。 在“项目”菜单上，单击“属性”。  
  
2.  上**编译**选项卡上，设置中的值**Option Strict**框。  
  
### <a name="conditions"></a> 若要在 IDE 中设置警告配置  
 当你使用[编译页，项目设计器 (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)而不是`Option Strict`语句中，你可以生成错误的条件的其他控制。 **警告配置**一部分**编译页**具有对应于三个条件会导致编译时错误的设置时`Option Strict`上。 这些设置如下：  
  
-   隐式转换  
  
-   晚期绑定；调用可能在运行时失败  
  
-   隐式类型；假定为对象  
  
 “Option Strict”设置为“开启”时，所有这三个警告配置设置都将被设置为“错误”。 “Option Strict”设置为“关闭”时，所有这三个设置都将被设置为“无”。  
  
 可单独将各个警告配置设置更改为“无”、“警告”或“错误”。 如果三个警告配置都设置为“错误”，则 `On` 会出现在 `Option strict` 框中。 如果三个都设置为“无”，则 `Off` 会出现在此框中。 对于这些配置的任何其他组合，显示“(自定义)”。  
  
### <a name="to-set-the-option-strict-default-setting-for-new-projects"></a>若要设置 Option Strict 的默认设置为新项目  
 创建项目时**Option Strict**上设置**编译**选项卡设置为**Option Strict**中设置**选项**对话框。  
  
 若要设置`Option Strict`在此对话框上**工具**菜单中，单击**选项**。 在“选项”对话框中，展开“项目和解决方案”，然后单击“VB 默认值”。 中的初始默认设置**VB 默认值**是`Off`。  
  
### <a name="to-set-option-strict-on-the-command-line"></a>若要在命令行上设置 Option Strict  
 包括[/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)中的编译器选项**vbc**命令。  
  
## <a name="example"></a>示例  
 下面的示例演示由收缩转换的隐式类型转换导致的编译时错误。 此类别的错误对应于**隐式转换**上的条件**编译页**。  
  
 [!code-vb[VbVbalrStatements#161](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class13.vb#161)]  
  
## <a name="example"></a>示例  
 下面的示例演示了编译时错误引起的后期绑定。 此类别的错误对应于**Late 绑定; 调用可能在运行时失败**上的条件**编译页**。  
  
 [!code-vb[VbVbalrStatements#162](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class13.vb#162)]  
  
## <a name="example"></a>示例  
 下面的示例演示使用的隐式类型声明的变量引起的错误`Object`。 此类别的错误对应于**隐式类型; 假定为对象**上的条件**编译页**。  
  
 [!code-vb[VbVbalrStatements#163](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class13.vb#163)]  
  
 [!code-vb[VbVbalrStatements#164](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class13.vb#164)]  
  
## <a name="see-also"></a>请参阅

- [扩大转换和收缩转换](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
- [隐式转换和显式转换](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
- [“项目设计器”->“编译”页 (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)
- [Option Explicit 语句](../../../visual-basic/language-reference/statements/option-explicit-statement.md)
- [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [如何：访问对象的成员](../../../visual-basic/programming-guide/language-features/variables/how-to-access-members-of-an-object.md)
- [XML 中的嵌入式表达式](../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)
- [宽松委托转换](../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)
- [Office 解决方案中的晚期绑定](/visualstudio/vsto/late-binding-in-office-solutions)
- [/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)
- [“选项”对话框 ->“项目”->“Visual Basic 默认值”](/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)
