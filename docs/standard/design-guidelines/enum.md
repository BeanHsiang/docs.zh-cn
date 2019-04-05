---
title: 枚举设计
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- type design guidelines, enumerations
- simple enumerations
- enumerations [.NET Framework], design guidelines
- class library design guidelines [.NET Framework], enumerations
- flags enumerations
ms.assetid: dd53c952-9d9a-4736-86ff-9540e815d545
author: KrzysztofCwalina
ms.openlocfilehash: c0645ba1179c4c6fd961b871b3061cd51174f427
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54675168"
---
# <a name="enum-design"></a>枚举设计
枚举是一种特殊的值类型。 枚举分为两种类型：简单枚举和标志枚举。  
  
 简单枚举表示小型的封闭选项集。 简单枚举的一个常见示例是一组颜色。  
  
 标志枚举旨在支持枚举值的按位运算。 标志枚举的一个常见示例是选项列表。  
  
 ✓ 务必将枚举用于强类型参数、属性和表示一组值集的返回值。  
  
 ✓ 务必首选使用枚举而不是静态常量。  
  
 X 切忌将枚举用于开放集（如操作系统版本、朋友的姓名等）。  
  
 X 切忌提供供将来使用的保留枚举值。  
  
 在后面的阶段，可以随时向现有枚举添加值。 有关向枚举添加值的更多详细信息，请参阅[向枚举添加值](#add_value)。 保留值只会污染实际的值集，并往往会导致用户错误。  
  
 X 避免公开暴露只有一个值的枚举。  
  
 确保 C API 未来可扩展性的常见做法是向方法签名添加保留参数。 这样的保留参数可以表示为具有单个默认值的枚举。 这不应该在托管 API 中完成。 方法重载允许在将来的版本中添加参数。  
  
 **X 切忌**在枚举中包括 sentinel 值。  
  
 虽然它们有时对框架开发人员很有帮助，但是 sentinel 值会给框架的用户造成混淆。 它们用于跟踪枚举的状态，而不是枚举表示的集合中的一个值。  
  
 **✓ 务必**为简单枚举提供零值。  
  
 考虑将值称为“None”等类似名称。 如果此类值不适合此特定枚举，则应为该枚举的最常见默认值指定为零的基础值。  
  
 **✓ 考虑**使用 <xref:System.Int32>（大多数编程语言中的默认值）作为枚举的基础类型，除非满足以下任何条件：  
  
-   枚举是一个标志枚举，包含 32 个以上标志，或者将来可能有更多标志。  
  
-   在枚举可能大小各不相同的情况下，基础类型需要与 <xref:System.Int32> 不同，以便更容易地与非托管代码进行互操作。  
  
-   较小的基础类型将大大节省空间。 如果希望将枚举主要用作控制流的参数，则大小差别不大。 如果符合以下条件，则可以大大节省空间：  
  
    -   希望将枚举在非常频繁实例化的结构或类中用作字段。  
  
    -   希望用户创建枚举实例的大型数组或集合。  
  
    -   希望序列化大量枚举实例。  
  
 对于内存中的用，请注意托管对象始终是 `DWORD` 对齐的，因此您需要在实例中有效地使用多个枚举或其他较小的结构来打包较小的枚举，这很重要，因为总实例大小总是要四舍五入到 `DWORD`。  
  
 **✓ 务必**为标志枚举使用复数名词或名词短语命名，为简单枚举使用单数名词或名词短语命名。  
  
 **X 切忌**直接扩展 <xref:System.Enum?displayProperty=nameWithType>。  
  
 <xref:System.Enum?displayProperty=nameWithType> 是 CLR 用于创建用户定义的枚举的特殊类型。 大多数编程语言都提供了一个编程元素，来使你可以使用此功能。 例如，在 C# 中，`enum` 关键字用于定义枚举。  
  
<a name="design"></a>   
### <a name="designing-flag-enums"></a>设计标志枚举  
 **✓ 务必**对标志枚举应用 <xref:System.FlagsAttribute?displayProperty=nameWithType>。 不要将此特性应用于简单枚举。  
  
 **✓ 务必**对标志枚举值使用 2 的幂，以便可以使用按位 OR 运算自由组合它们。  
  
 **✓ 考虑**为常用的标志组合提供特殊的枚举值。  
  
 按位运算是一种高级概念，简单任务应无需使用。 <xref:System.IO.FileAccess.ReadWrite> 就是这种特殊值的一个例子。  
  
 **X 避免**创建某些值组合无效的标志枚举。  
  
 **X 避免**使用值为零的标志枚举，除非该值表示“已清除所有标志”，并按照下一指南的规定进行适当命名。  
  
 ✓ 务必将值为零的标志枚举命名为 `None`。 于标志枚举，该值必须始终表示“已清除所有标志”。  
  
<a name="add_value"></a>   
### <a name="adding-value-to-enums"></a>将值添加到枚举  
 你常常会发现，需要在已发布枚举后向其添加一个值。 从现有 API 返回新添加的值时，会存在潜在的应用程序兼容性问题，因为编写不当的应用程序可能无法正确处理新值。  
  
 ✓ 考虑将值添加到枚举，监管存在较低的兼容性风险。  
  
 如果已获得了有关向枚举添加值而引起的应用程序不兼容性问题的实际数据，请考虑添加可返回新值和旧值的新 API，并弃用旧 API，该旧 API 应会继续仅返回旧值。 这将确保现有的应用程序保持兼容。  
  
 *部分版权 © 2005, 2009 Microsoft Corporation。保留所有权利。*  
  
 *经 Pearson Education, Inc 授权，转载自[框架设计准则：可重用的 .NET 库的约定、习惯用语和模式，第 2 版](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 作者：Krzysztof Cwalina 和 Brad Abrams，由 Addison Wesley Professional 于 2008 年 10 月 22 日印发，作为 Microsoft Windows 开发系列的一部分。*  
  
## <a name="see-also"></a>请参阅

- [类型设计准则](../../../docs/standard/design-guidelines/type.md)
- [框架设计指南](../../../docs/standard/design-guidelines/index.md)
