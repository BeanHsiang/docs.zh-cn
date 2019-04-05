---
title: AttributeUsage (C#)
ms.date: 04/25/2018
ms.openlocfilehash: a3a82e33d7259ec56ec3e907bc3d4d9f8a01167d
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54589303"
---
# <a name="attributeusage-c"></a>AttributeUsage (C#)

确定如何使用自定义特性类。 <xref:System.AttributeUsageAttribute> 是应用到自定义特性定义的特性。 `AttributeUsage` 特性帮助控制：

- 可能应用到的具体程序元素特性。 除非使用限制，否则特性可能应用到以下任意程序元素：
  - 程序集
  - name
  - Field — 字段
  - Event — 事件
  - 方法
  - param
  - 属性
  - return
  - 类型
- 某特性是否可多次应用于单个程序元素。
- 特性是否由派生类继承。

显式应用时，默认设置如以下示例所示：

[!code-csharp[Define a new attribute](../../../../../samples/snippets/csharp/attributes/NewAttribute.cs#1)]

在此示例中，`NewAttribute` 类可应用于任何受支持的程序元素。 但是它对每个实体仅能应用一次。 特性应用于基类时，它由派生类继承。

<xref:System.AttributeUsageAttribute.AllowMultiple> 和 <xref:System.AttributeUsageAttribute.Inherited> 参数是可选的，因此以下代码具有相同效果：

[!code-csharp[Omit optional attributes](../../../../../samples/snippets/csharp/attributes/NewAttribute.cs#2)]

第一个 <xref:System.AttributeUsageAttribute> 参数必须是 <xref:System.AttributeTargets> 枚举的一个或多个元素。 可将多个目标类型与 OR 运算符链接在一起，如下例所示：

[!code-csharp[Create an attribute for fields or properties](../../../../../samples/snippets/csharp/attributes/NewPropertyOrFieldAttribute.cs#1)]

从 C# 7.3 开始，特性可应用于自动实现的属性的属性或支持字段。 特性应用于属性，除非在特性上指定 `field` 说明符。 都在以下示例中进行了演示：

[!code-csharp[Create an attribute for fields or properties](../../../../../samples/snippets/csharp/attributes/NewPropertyOrFieldAttribute.cs#2)]

如果 <xref:System.AttributeUsageAttribute.AllowMultiple> 参数为 `true`，那么结果特性可多次应用于单个实体，如以下示例所示：

[!code-csharp[Create and use an attribute that can be applied multiple times](../../../../../samples/snippets/csharp/attributes/MultiUseAttribute.cs#1)]

在本例中，`MultiUseAttribute` 可重复应用，因为 `AllowMultiple` 设置为 `true`。 所显示的两种用于应用多个特性的格式均有效。

如果 <xref:System.AttributeUsageAttribute.Inherited> 为 `false`，那么该特性不是由特性类派生的类继承。 例如:

[!code-csharp[Create and use an attribute that can be applied multiple times](../../../../../samples/snippets/csharp/attributes/NonInheritedAttribute.cs#1)]

在本例中，`NonInheritedAttribute` 不会通过继承应用于 `DClass`。

## <a name="remarks"></a>备注

`AttributeUsage` 特性是单次使用的特性 -- 它无法应用于同一个类超过一次。 `AttributeUsage` 是 <xref:System.AttributeUsageAttribute> 的别名。

有关详细信息，请参阅[使用反射访问特性 (C#)](accessing-attributes-by-using-reflection.md)。

## <a name="example"></a>示例

以下示例演示 <xref:System.AttributeUsageAttribute.Inherited> 和 <xref:System.AttributeUsageAttribute.AllowMultiple> 参数对 <xref:System.AttributeUsageAttribute> 特性的影响，以及如何枚举应用于类的自定义特性。

[!code-csharp[Applying and querying attributes](../../../../../samples/snippets/csharp/attributes/Program.cs#1)]

## <a name="sample-output"></a>示例输出

```text
Attributes on Base Class:
FirstAttribute
SecondAttribute
Attributes on Derived Class:
ThirdAttribute
ThirdAttribute
SecondAttribute
```

## <a name="see-also"></a>请参阅

- <xref:System.Attribute>
- <xref:System.Reflection>
- [C# 编程指南](../..//index.md)
- [特性](../../../..//standard/attributes/index.md)
- [反射 (C#)](../reflection.md)
- [特性](index.md)
- [创建自定义特性 (C#)](creating-custom-attributes.md)
- [使用反射访问特性 (C#)](accessing-attributes-by-using-reflection.md)
