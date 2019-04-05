---
title: 运算符重载
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- operators [.NET Framework], overloads
- names [.NET Framework], overloaded operators
- member design guidelines, operators
- overloaded operators
ms.assetid: 37585bf2-4c27-4dee-849a-af70e3338cc1
author: KrzysztofCwalina
ms.openlocfilehash: 441dc2777cd8d221300c526b6b31a647af60ca71
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54646573"
---
# <a name="operator-overloads"></a>运算符重载
运算符重载允许框架类型的外观类似内置语言基元。  
  
 虽然在某些情况下允许使用运算符重载并且有用，但应谨慎使用。 在许多情况下，运算符重载受到滥用，例如框架设计者开始使用运算符进行本应是简单方法的操作。 以下准则可帮助你确定何时以及如何使用运算符重载。  
  
 **X 避免**定义运算符重载，但对于看似基元（内置）类型的类型除外。  
  
 **✓ 考虑**在一个感觉应该像基元类型的类型中定义运算符重载。  
  
 例如，<xref:System.String?displayProperty=nameWithType> 定义 `operator==` 和 `operator!=`。  
  
 **✓ 务必**在表示数字的结构中定义运算符重载（例如 <xref:System.Decimal?displayProperty=nameWithType> ）。  
  
 **X 切忌**在定义运算符重载时过于刻意。  
  
 如果操作结果直观而明显，则运算符重载非常有用。 例如，能够从一个 <xref:System.DateTime> 中减去另一个 `DateTime`，并得到 <xref:System.TimeSpan>，这是有意义的。 但是，使用逻辑 union 运算符来合并两个数据库查询或使用 shift 运算符写入流则是不合适的。  
  
 **X 切忌**提供运算符重载，除非至少其中一个运算数是定义重载的类型。  
  
 **X 切忌**在定义运算符重载时过于刻意。  
  
 例如，如果重载了 `operator==`，则还应该重载 `operator!=`。 同样，如果重载了 `operator<`，则还应该重载 `operator>`，以此类推。  
  
 **✓ 考虑**提供与每个重载运算符对应的具有友好名称的方法。  
  
 许多语言不支持运算符重载。 因此，建议重载运算符的类型包括具有适当的特定于域的名称的辅助方法，该方法提供等效功能。  
  
 下表包含一系列运算符和相应的友好方法名称。  
  
|C# 运算符符号|元数据名称|友好名称|  
|-------------------------|-------------------|-------------------|  
|`N/A`|`op_Implicit`|`To<TypeName>/From<TypeName>`|  
|`N/A`|`op_Explicit`|`To<TypeName>/From<TypeName>`|  
|`+ (binary)`|`op_Addition`|`Add`|  
|`- (binary)`|`op_Subtraction`|`Subtract`|  
|`* (binary)`|`op_Multiply`|`Multiply`|  
|`/`|`op_Division`|`Divide`|  
|`%`|`op_Modulus`|`Mod or Remainder`|  
|`^`|`op_ExclusiveOr`|`Xor`|  
|`& (binary)`|`op_BitwiseAnd`|`BitwiseAnd`|  
|<code>&#124;</code>|`op_BitwiseOr`|`BitwiseOr`|  
|`&&`|`op_LogicalAnd`|`And`|  
|<code>&#124;&#124;</code>|`op_LogicalOr`|`Or`|  
|`=`|`op_Assign`|`Assign`|  
|`<<`|`op_LeftShift`|`LeftShift`|  
|`>>`|`op_RightShift`|`RightShift`|  
|`N/A`|`op_SignedRightShift`|`SignedRightShift`|  
|`N/A`|`op_UnsignedRightShift`|`UnsignedRightShift`|  
|`==`|`op_Equality`|`Equals`|  
|`!=`|`op_Inequality`|`Equals`|  
|`>`|`op_GreaterThan`|`CompareTo`|  
|`<`|`op_LessThan`|`CompareTo`|  
|`>=`|`op_GreaterThanOrEqual`|`CompareTo`|  
|`<=`|`op_LessThanOrEqual`|`CompareTo`|  
|`*=`|`op_MultiplicationAssignment`|`Multiply`|  
|`-=`|`op_SubtractionAssignment`|`Subtract`|  
|`^=`|`op_ExclusiveOrAssignment`|`Xor`|  
|`<<=`|`op_LeftShiftAssignment`|`LeftShift`|  
|`%=`|`op_ModulusAssignment`|`Mod`|  
|`+=`|`op_AdditionAssignment`|`Add`|  
|`&=`|`op_BitwiseAndAssignment`|`BitwiseAnd`|  
|<code>&#124;=</code>|`op_BitwiseOrAssignment`|`BitwiseOr`|  
|`,`|`op_Comma`|`Comma`|  
|`/=`|`op_DivisionAssignment`|`Divide`|  
|`--`|`op_Decrement`|`Decrement`|  
|`++`|`op_Increment`|`Increment`|  
|`- (unary)`|`op_UnaryNegation`|`Negate`|  
|`+ (unary)`|`op_UnaryPlus`|`Plus`|  
|`~`|`op_OnesComplement`|`OnesComplement`|  
  
### <a name="overloading-operator-"></a>重载运算符 ==  
 重载 `operator ==` 非常复杂。 运算符的语义需要与其他几个其他成员兼容，如 <xref:System.Object.Equals%2A?displayProperty=nameWithType>。  
  
### <a name="conversion-operators"></a>转换运算符  
 转换运算符是一元运算符，允许从一种类型转换为另一种类型。 必须在操作数或返回类型上将运算符定义为静态成员。 有两种类型的转换运算符：隐式和显式。  
  
 **X 切忌**提供转换运算符，如果最终用户未明确要求这种转换。  
  
 **X 切忌**定义类型域外的转换运算符。  
  
 例如， <xref:System.Int32>、<xref:System.Double> 和 <xref:System.Decimal> 都是数字类型，而 <xref:System.DateTime> 不是。 因此，不应该存在将 `Double(long)` 转换到 `DateTime` 的转换运算符。 在这种情况中，应该首选构造函数。  
  
 **X 切忌**在转换可能产生损耗的情况下提供隐式转换运算符。  
  
 例如，不应该存在从 `Double` 到 `Int32` 的隐式转换，因为 `Double` 比 `Int32` 的范围更大。 可以提供显式转换运算符，即使转换可能产生损耗。  
  
 **X 切忌**从隐式转换中引发异常。  
  
 最终用户将难以理解当前出现的情况，因为他们可能不知道转换正在进行。  
  
 **✓ 务必**引发 <xref:System.InvalidCastException?displayProperty=nameWithType>，如果对转换运算符的调用会导致有损转换，并且运算符的协定不允许丢失数据的转换。  
  
 *部分版权 © 2005, 2009 Microsoft Corporation。保留所有权利。*  
  
 *经 Pearson Education, Inc 授权，转载自[框架设计准则：可重用的 .NET 库的约定、习惯用语和模式，第 2 版](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 作者：Krzysztof Cwalina 和 Brad Abrams，由 Addison Wesley Professional 于 2008 年 10 月 22 日印发，作为 Microsoft Windows 开发系列的一部分。*  
  
## <a name="see-also"></a>请参阅

- [成员设计准则](../../../docs/standard/design-guidelines/member.md)
- [框架设计指南](../../../docs/standard/design-guidelines/index.md)
