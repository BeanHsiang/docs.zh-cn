---
title: 参数设计
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- member design guidelines [.NET Framework], parameters
- members [.NET Framework], parameters
- names [.NET Framework], parameters
- parameters, design guidelines
- reserved parameters
ms.assetid: 3f33bf46-4a7b-43b3-bb78-1ffebe0dcfa6
author: KrzysztofCwalina
ms.openlocfilehash: 5a0f6e0fab5d0f2fe8574e348fc6b8ae726eeb99
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54617208"
---
# <a name="parameter-design"></a>参数设计
本部分提供了有关参数设计的广泛准则，包括用于检查参数的准则。 此外，还应参考[命名参数](../../../docs/standard/design-guidelines/naming-parameters.md)中介绍的准则。  
  
 **✓ 务必**使用可提供成员所需功能的最少的派生参数类型。  
  
 例如，假设想要设计一个枚举集合并将每个项输出到控制台的的方法。 此类方法应使用 <xref:System.Collections.IEnumerable> 作为参数，而不应使用 <xref:System.Collections.ArrayList> 或 <xref:System.Collections.IList>。  
  
 **X 切忌**使用保留参数。  
  
 如果在将来的某个版本中需要对成员有更多输入，则可以添加新的重载。  
  
 **X 切忌**使用将指针、指针数组或多维数组作为参数的公开方法。  
  
 指针和多维数组相对难以正确使用。 几乎在所有情况下，都可以重新设计 API 以避免将这些类型作为参数。  
  
 **✓ 务必**把所有 `out` 参数放置在所有传值和 `ref` 参数（不包括参数数组）之后，即使它会导致重载之间参数排序的不一致（请参阅[成员重载](../../../docs/standard/design-guidelines/member-overloading.md)）。  
  
 可以将 `out` 参数看作是额外的返回值，并且可以将它们分组在一起，使方法签名更易于理解。  
  
 **✓ 务必**在重写成员或实现接口成员时，在命名参数上保持一致。  
  
 这更好地传达了方法之间的关系。  
  
### <a name="choosing-between-enum-and-boolean-parameters"></a>在枚举和布尔形参之间进行选择  
 **✓ 务必**使用枚举，如果成员有两个或多个布尔参数的话。  
  
 **X 切忌**使用布尔值，除非绝对确定永远不需要两个以上的值。  
  
 枚举为你将来添加值提供了一些空间，但应该注意在枚举中添加值的所有影响，这些内容在[枚举设计](../../../docs/standard/design-guidelines/enum.md)中进行了描述。  
  
 **✓ 考虑**使用布尔值作为构造函数参数，这些参数是真正的双状态值，仅用于初始化布尔属性。  
  
### <a name="validating-arguments"></a>验证实参  
 **✓ 务必**验证传递到公共、受保护或显式实现的成员的实参。 如果验证失败，将引发 <xref:System.ArgumentException?displayProperty=nameWithType> 或其一个子类。  
  
 请注意，实际验证不一定必须在公共成员或受保护成员本身中进行。 它可能发生在某些私有或内部例程的较低级别。 重点是暴露给最终用户的整个上层区域会检查参数。  
  
 **✓ 务必**引发 <xref:System.ArgumentNullException>，如果传递 null 实参且该成员不支持 null 实参。  
  
 **✓ 务必**验证 enum 形参。  
  
 不要假设枚举实参将在枚举定义的范围内。 CLR 允许将任何整数值转换为枚举值，即使该值未在枚举中定义。  
  
 **X 切忌**将 <xref:System.Enum.IsDefined%2A?displayProperty=nameWithType> 用于枚举范围检查。  
  
 **✓ 务必**注意，可变实参在验证后可能已更改。  
  
 如果该成员对安全性敏感，则建议生成一个副本，然后验证并处理该实参。  
  
### <a name="parameter-passing"></a>参数传递  
 从框架设计者的角度来看，有三组主要形参：传值形参、`ref` 形参和 `out` 形参。  
  
 当实参通过传值形参传递时，该成员将接收传入的实际实参的副本。 如果实参是值类型，则将实参的副本放在栈上。 如果实参是引用类型，则将引用的副本放在栈上。 最常用的 CLR 语言，如 C#，VB.NET 和 C++，默认按值传递形参。  
  
 当实参通过 `ref` 形参传递时，成员接收对传入的实际实参的引用。 如果实参是值类型，则将实参的引用放在栈上。 如果实参是引用类型，则将引用的引用放在栈上。 `Ref` 形参可用于允许成员修改调用方传递的实参。  
  
 `Out`形参类似于`ref`形参，但存在一些细微差异。 该形参最初被视为未分配，并且在为其分配某个值之前无法在成员体内中读取。 此外，必须在成员返回之前为形参指定一些值。  
  
 **X 避免**使用 `out` 或 `ref` 形参。  
  
 使用 `out` 或 `ref` 形参需要一些经验，包括使用指针，理解值类型和引用类型的不同，以及处理具有多个返回值的方法。 另外，`out` 和 `ref` 形参之间的区别并不广为人知。 为一般用户设计的框架架构师不应期望用户熟练掌握使用 `out` 或 `ref` 形参。  
  
 **X 切忌**通过引用传递引用类型。  
  
 该规则有一些有限的例外情况，例如可用于交换引用的方法。  
  
### <a name="members-with-variable-number-of-parameters"></a>具有可变形参数量的成员  
 可以通过提供数组形参来表示使用可变数量实参的成员。 例如，<xref:System.String> 提供了以下方法：  
  
```  
public class String {  
    public static string Format(string format, object[] parameters);  
}  
```  
  
 然后，用户可以调用<xref:System.String.Format%2A?displayProperty=nameWithType>方法，按如下所示：  
  
 `String.Format("File {0} not found in {1}",new object[]{filename,directory});`  
  
 将 C# params 关键字添加到数组形参会将形参更改为所谓的 params 数组形参，并提供了创建临时数组的快捷方式。  
  
```  
public class String {  
    public static string Format(string format, params object[] parameters);  
}  
```  
  
 执行此操作允许用户通过直接在实参列表中传递数组元素来调用方法。  
  
 `String.Format("File {0} not found in {1}",filename,directory);`  
  
 请注意，params 关键字只能添加到形参列表中的最后一个形参。  
  
 **✓ 考虑**如果希望最终用户传递具有少量元素的数组，则将 params 关键字添加到数组形参中。 如果期望在常见场景中传递大量元素，则用户可能无论如何也不会以内联方式传递这些元素，因此 params 关键字不是必需的。  
  
 **X 避免**使用 params 数组，如果调用方几乎总是将输入放在数组中。  
  
 例如，具有字节数组形参的成员几乎不会通过传递单个字节来调用。 因此，.NET Framework 中的字节数组形参不使用 params 关键字。  
  
 **X 切忌**使用 params 数组，如果采用 params 数组形参的成员修改了数组。  
  
 由于许多编译器将成员的实参转换为调用站点的临时数组，因此该数组可能是临时对象，所以对数组的任何修改都将丢失。  
  
 **✓ 考虑**在简单的重载中使用 params 关键字，即使更复杂的重载不能使用它。  
  
 问问自己用户是否会重视在一个重载中使用 params 数组，即使它不在所有重载中。  
  
 **✓ 务必**尝试对形参进行排序，以使其可以使用 params 关键字。  
  
 **✓ 考虑**在性能极其敏感的 API 中为具有少量实参的调用提供特殊的重载和代码路径。  
  
 这样在使用少量实参调用 API 时可以避免创建数组对象。 通过采用数组形参的单数形式，并添加数字后缀来形成形参的名称。  
  
 应该只在对整个代码路径执行特例时才这样做，而不仅仅是创建一个数组并调用更通用的方法。  
  
 **✓ 务必**注意，null 可以作为 params 数组实参传递。  
  
 应该在处理之前验证数组是否为 null。  
  
 **X 切忌**使用 `varargs` 方法，也称为省略号。  
  
 某些 CLR 语言，如 C++ ，支持传递变量形参列表的替代约定，称为 `varargs` 方法。 该约定不应在框架中使用，因为它不符合CLS。  
  
### <a name="pointer-parameters"></a>指针参数  
 通常，指针不应出现在设计良好的托管代码框架的公共上层区域中。 大多数情况下，指针应该被封装。 但是，在某些情况下，出于互操作性原因需要指针，在这种情况下适合使用指针。  
  
 **✓ 务必**为所有采用指针实参的成员提供替代方法，因为指针不符合 CLS。  
  
 **X 避免**对指针实参进行高开销的实参检查。  
  
 **✓ 务必**在设计带指针的成员时，遵循常见的指针相关约定。  
  
 例如，不需要传递起始索引，因为可以使用简单的指针算法来完成相同的结果。  
  
 *部分版权 © 2005, 2009 Microsoft Corporation。保留所有权利。*  
  
 *经 Pearson Education, Inc 授权，转载自[框架设计准则：可重用的 .NET 库的约定、习惯用语和模式，第 2 版](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 作者：Krzysztof Cwalina 和 Brad Abrams，由 Addison Wesley Professional 于 2008 年 10 月 22 日印发，作为 Microsoft Windows 开发系列的一部分。*  
  
## <a name="see-also"></a>请参阅

- [成员设计准则](../../../docs/standard/design-guidelines/member.md)
- [框架设计指南](../../../docs/standard/design-guidelines/index.md)
