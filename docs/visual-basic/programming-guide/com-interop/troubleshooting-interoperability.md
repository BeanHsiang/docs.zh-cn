---
title: 互操作性疑难解答 (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- interop, deploying assemblies
- assemblies [Visual Basic]
- interop, installing assemblies that share components
- COM objects, troubleshooting
- interop, sharing components
- troubleshooting interoperability [Visual Basic]
- interoperability, troubleshooting
- COM interop [Visual Basic], troubleshooting
- assemblies [Visual Basic], deploying
- troubleshooting Visual Basic, interoperability
- interop assemblies
- interoperability, sharing components
- shared components, using with assemblies
ms.assetid: b324cc1e-b03c-4f39-aea6-6a6d5bfd0e37
ms.openlocfilehash: 197361020ad8c6a88a5fc8617b8e24f420799e14
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57377092"
---
# <a name="troubleshooting-interoperability-visual-basic"></a>互操作性疑难解答 (Visual Basic)
当 COM 和托管的代码之间互操作[!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)]，可能会遇到一个或多个以下常见的问题。  
  
## <a name="vbconinteroperabilitymarshalinganchor1"></a> 互操作封送处理  
 有时，您可能需要使用数据类型不属于[!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)]。 互操作程序集来处理大多数的 COM 对象的工作，但您可能要控制对 COM 公开托管的对象时使用的数据类型 例如，类库中的结构必须指定`BStr`非托管字符串发送到创建的 Visual Basic 6.0 和早期版本的 COM 对象的类型。 在这种情况下，可以使用<xref:System.Runtime.InteropServices.MarshalAsAttribute>属性会导致托管的类型作为非托管类型公开。  
  
## <a name="vbconinteroperabilitymarshalinganchor2"></a> 导出到非托管代码的固定长度字符串  
 在 Visual Basic 6.0 和早期版本中，字符串到 COM 对象导出为不带 null 终止字符的字节序列。 对于与其他语言的兼容性，Visual Basic.NET 包括终止字符输出字符串时。 若要解决此不兼容性的最佳方式是将缺少的终止字符的数组作为字符串导出`Byte`或`Char`。  
  
## <a name="vbconinteroperabilitymarshalinganchor3"></a> 导出继承层次结构  
 托管的类层次结构平展时公开为 COM 对象。 例如，如果你的成员，定义一个基类，然后继承的基类中派生的类公开为 COM 对象使用派生的类中的 COM 对象的客户端将不能使用继承的成员。 可以从 COM 对象只能作为基类的实例访问基类成员，然后仅当该基类还创建为 COM 对象。  
  
## <a name="overloaded-methods"></a>重载方法  
 尽管可以使用 Visual Basic 创建重载的方法，但它们不支持通过 com。 当包含重载的方法的类公开为 COM 对象时，重载方法生成新的方法名称。  
  
 例如，考虑具有两个重载的类，`Synch`方法。 当类公开为 COM 对象时，可能是新生成的方法名`Synch`和`Synch_2`。  
  
 重命名可能会导致为 COM 对象的使用者的两个问题。  
  
1.  客户端可能不希望生成的方法名称。  
  
2.  新重载添加到类或其基本类时，可以更改中公开为 COM 对象的类的生成的方法名称。 这会导致版本控制问题。  
  
 若要解决这两个问题，请为每个方法提供一个唯一的名称，而不是使用重载，开发时将公开为 COM 对象的对象。  
  
## <a name="vbconinteroperabilitymarshalinganchor4"></a> 使用通过互操作程序集的 COM 对象  
 几乎就像它们是托管的代码替换它们所表示的 COM 对象使用互操作程序集。 但是，由于它们是包装器和不是实际的 COM 对象，是使用互操作程序集和标准程序集之间的一些差异。 这些不同之处包括类、 和参数和返回值的数据类型的风险。  
  
## <a name="vbconinteroperabilitymarshalinganchor5"></a> 类公开为这两个接口和类  
 与标准的程序集中的类，不同的 COM 类在互操作程序集作为一个接口和类，用以表示的 COM 类中公开。 接口的名称完全相同的 COM 类。 互操作的类的名称是相同的原始 COM 类，但以单词"类"追加。 例如，假设您的项目必须具有对 COM 对象的互操作程序集的引用。 如果 COM 类命名为`MyComClass`，IntelliSense 和对象浏览器显示名为接口`MyComClass`和名为的类`MyComClassClass`。  
  
## <a name="vbconinteroperabilitymarshalinganchor6"></a> 创建.NET Framework 类的实例  
 通常情况下，创建的实例[!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)]类使用`New`语句和类名。 互操作程序集所表示的 COM 类是在其中可以使用的一个例子`New`语句用于接口。 除非你使用的 COM 类`Inherits`语句，就像类一样，可以使用该接口。 下面的代码演示如何创建`Command`具有对 Microsoft ActiveX 数据对象 2.8 库 COM 对象的引用的项目中的对象：  
  
 [!code-vb[VbVbalrInterop#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#20)]  
  
 但是，如果你使用 COM 类作为基的派生类，必须使用互操作表示的类的 COM 类，如以下代码所示：  
  
 [!code-vb[VbVbalrInterop#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#21)]  
  
> [!NOTE]
>  互操作程序集隐式实现表示 COM 类的接口。 不应尝试使用`Implements`将导致语句来实现这些接口或错误。  
  
## <a name="vbconinteroperabilitymarshalinganchor7"></a> 有关参数和返回值的数据类型  
 与标准的程序集的成员，互操作程序集的成员可能具有不同于原始对象声明中使用的数据类型。 尽管互操作程序集隐式转换为兼容的公共语言运行时类型的 COM 类型，但您应注意两面用于避免运行时错误的数据类型。 例如，在 Visual Basic 6.0 和早期版本中，类型的值中创建的 COM 对象`Integer`假定[!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)]等效类型`Short`。 建议使用对象浏览器来检查导入的成员的特征之后使用它们。  
  
## <a name="vbconinteroperabilitymarshalinganchor8"></a> 模块级别 COM 方法  
 由大多数 COM 对象创建的 COM 类实例`New`关键字，然后再调用对象的方法。 此规则的例外涉及 COM 对象，包含`AppObj`或`GlobalMultiUse`COM 类。 此类类类似于 Visual Basic.NET 类中的模块级方法。 Visual Basic 6.0 和早期版本隐式创建的此类对象的实例为您第一次调用其方法之一。 例如，在 Visual Basic 6.0 中可以添加到 Microsoft DAO 3.6 对象库，并调用引用`DBEngine`而无需首先创建的实例的方法：  
  
```vb  
Dim db As DAO.Database  
' Open the database.  
Set db = DBEngine.OpenDatabase("C:\nwind.mdb")  
' Use the database object.  
```  
  
 Visual Basic.NET 要求，始终可以使用其方法之前创建的 COM 对象的实例。 若要在 Visual Basic 中使用这些方法，声明的变量的所需的类，并使用新关键字来将对象分配给对象变量。 `Shared`时想要确保可以使用关键字创建只有一个类的实例。  
  
 [!code-vb[VbVbalrInterop#23](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#23)]  
  
## <a name="vbconinteroperabilitymarshalinganchor9"></a> 事件处理程序中未处理的错误  
 一个常见的互操作问题涉及处理引发的 COM 对象事件的事件处理程序中的错误。 此类错误将被忽略，除非您专门检查使用的错误`On Error`或`Try...Catch...Finally`语句。 例如，下面的示例是从 Visual Basic.NET 项目具有对 Microsoft ActiveX 数据对象 2.8 库 COM 对象的引用。  
  
 [!code-vb[VbVbalrInterop#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#24)]  
  
 此示例将按预期方式引发错误。 但是，如果尝试不相同的示例`Try...Catch...Finally`块中，错误将忽略就使用`OnError Resume Next`语句。 如果没有错误处理机制，被零除将以静默方式失败。 此类错误永远不会引发未处理的异常错误，因为它是异常的使用某种形式处理从 COM 对象的事件的事件处理程序中处理的重要。  
  
### <a name="understanding-com-interop-errors"></a>了解 COM 互操作错误  
 如果没有错误处理机制，互操作调用通常生成错误可提供很少信息。 只要可能，使用结构化处理，以提供有关问题的详细信息，它们出现的错误。 调试应用程序时，这可以是特别有用。 例如：  
  
 [!code-vb[VbVbalrInterop#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#25)]  
  
 可以通过检查异常对象的内容来查找错误说明、 HRESULT 和 COM 错误的原因等信息。  
  
## <a name="vbconinteroperabilitymarshalinganchor10"></a> ActiveX 控件问题  
 使用 Visual Basic 6.0 的大多数 ActiveX 控件与 Visual Basic.NET 配合使用不费力。 主要的例外是容器控件中或直观地包含其他控件的控件。 将无法正常使用 Visual Studio 的较旧控件的一些示例如下所示：  
  
-   Microsoft Forms 2.0 框架控件  
  
-   Up-down 控件，也称为数值调节钮控件  
  
-   Sheridan 选项卡控件  
  
 有仅几个解决方法不受支持 ActiveX 控件问题。 如果您拥有原始源代码，可以将现有控件迁移到 Visual Studio。 否则，可以检查与软件供应商的更新。NET 兼容版本的控件来替换不受支持的 ActiveX 控件。  
  
## <a name="vbconinteroperabilitymarshalinganchor11"></a> 控件 ByRef 传递 ReadOnly 属性  
 Visual Basic.NET 传递时有时会引发 COM 错误，例如，"错误 0x800A017F CTL_E_SETNOTSUPPORTED"`ReadOnly`属性的某些较旧的 ActiveX 控件，如`ByRef`其他过程的参数。 从 Visual Basic 6.0 的过程调用不会引发错误，并像按值传递，参数的处理方式类似。 Visual Basic.NET 错误消息指示您尝试更改一个属性，它不具有属性`Set`过程。  
  
 如果你有权访问所调用的过程，您可以通过使用来防止出现此错误`ByVal`关键字来声明接受的参数`ReadOnly`属性。 例如：  
  
 [!code-vb[VbVbalrInterop#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#26)]  
  
 如果你没有访问源代码的被调用的过程，您可以强制要通过添加一组额外的方括号调用过程通过值传递的属性。 例如，在项目中具有对 Microsoft ActiveX 数据对象 2.8 库 COM 对象的引用，您可以使用：  
  
 [!code-vb[VbVbalrInterop#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#27)]  
  
## <a name="vbconinteroperabilitymarshalinganchor12"></a> 部署公开互操作的程序集  
 部署公开的 COM 接口的程序集提供了一些独特的挑战。 例如，单独的应用程序引用相同的 COM 程序集时发生的潜在问题。 安装新版本的程序集和另一个应用程序仍在使用旧版本的程序集时，这种情况很常见。 如果您卸载共享某个 DLL 程序集，您可以无意中使其不可用到其他程序集。  
  
 若要避免此问题，应安装到全局程序集缓存 (GAC) 中的共享的程序集和组件使用合并模块。 如果您不能在 GAC 中安装应用程序，它应安装到 CommonFilesFolder 特定于版本的子目录中。  
  
 不共享的程序集应位于与调用应用程序目录中的并排显示。  
  
## <a name="see-also"></a>请参阅

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [COM 互操作](../../../visual-basic/programming-guide/com-interop/index.md)
- [Tlbimp.exe（类型库导入程序）](../../../framework/tools/tlbimp-exe-type-library-importer.md)
- [Tlbexp.exe（类型库导出程序）](../../../framework/tools/tlbexp-exe-type-library-exporter.md)
- [演练：使用 COM 对象实现继承](../../../visual-basic/programming-guide/com-interop/walkthrough-implementing-inheritance-with-com-objects.md)
- [Inherits 语句](../../../visual-basic/language-reference/statements/inherits-statement.md)
- [全局程序集缓存](../../../framework/app-domains/gac.md)
