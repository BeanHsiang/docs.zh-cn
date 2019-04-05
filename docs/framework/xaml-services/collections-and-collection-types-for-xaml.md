---
title: XAML 的集合类型
ms.date: 03/30/2017
ms.assetid: 58f8e7c6-9a41-4f25-8551-c042f1315baa
ms.openlocfilehash: 4123b64545f7c47a96c4cae496046a89b7e576b0
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57494618"
---
# <a name="collections-and-collection-types-for-xaml"></a>XAML 的集合类型

本主题介绍如何定义旨在支持一个集合，并以支持 XAML 语法用于实例化作为父对象元素或属性元素的子元素的集合项的类型的属性。

## <a name="xaml-collection-concepts"></a>XAML 集合概念

从概念上讲，任何关系中其中有多个作用域内的 XAML 对象元素的子项目或 XAML 属性元素必须实现为集合的 XAML。 该集合必须与该关系中的父级的 XAML 类型的特定 XAML 属性相关联。 该属性必须是集合，因为 XAML 处理器需要分配标记为新添加的项的支持集合属性中的每个项。

在 XAML 语言级别，集合支持的确切要求未完全定义。 集合可以是列表或字典 （而不是两者） 的概念定义 XAML 语言级别，但后备类型表示任一列表或字典不由 XAML 语言定义。

在.NET Framework XAML 服务中，按照后备类型的.NET Framework 更清楚地定义 XAML 集合支持的概念。 具体而言，集合的 XAML 支持基于多个.NET Framework 概念和 Api，它们对于列表和在常规的.NET Framework 编程的字典。

1. <xref:System.Collections.IList>接口指示列表集合。

2. <xref:System.Collections.IDictionary>接口指示字典集合。

3. <xref:System.Array> 表示一个数组和数组支持<xref:System.Collections.IList>方法。

在每个集合概念，.NET Framework XAML 服务 XAML 处理器需要调用`Add`集合属性的类型的特定实例上的方法。 或者，在序列化方案中，XAML 处理器生成的每个项列表、 字典或数组基于每个集合的特定概念的"项"中的离散 XAML 类型实例。 这些是： <xref:System.Collections.IList.Item%2A>;<xref:System.Collections.IDictionary.Item%2A>; 显式<xref:System.Array.System%23Collections%23IList%23Item%2A>为<xref:System.Array>。

## <a name="generic-collections"></a>泛型集合

泛型集合可用于常规.NET Framework 编程，并且还可用于 XAML 集合属性。 但是，泛型接口<xref:System.Collections.Generic.IList%601>并<xref:System.Collections.Generic.IDictionary%602>不识别的视为等效于非泛型的.NET Framework XAML 服务 XAML 处理器<xref:System.Collections.IList>或<xref:System.Collections.IDictionary>。 而不是实现接口，泛型集合属性类型的建议的方法是从类派生<xref:System.Collections.Generic.List%601>或<xref:System.Collections.Generic.Dictionary%602>。 这些类实现非泛型接口，并因此在基实现中包含 XAML 集合的预期的支持。

## <a name="read-only-collections-and-initialization-logic"></a>只读集合和初始化逻辑

在.NET Framework 编程，它是常见的设计模式，以使任何属性，保存集合为只读集合的值。 此模式允许拥有更好地控制集合会发生什么情况的集合属性的实例... 具体而言，该模式通过将属性设置阻止意外替换整个预先存在的收集。 在此模式下，对由调用方的集合的任何访问而是应将通过调用方法或属性，如支持的集合类型和/或相关集合接口<xref:System.Collections.IList>。

使用此模式意味着任何公开的只读集合属性的类必须先初始化该属性，包含一个空集合。 通常作为类的构造行为的一部分执行初始化。 可用于 XAML，它很重要，默认构造函数中，始终引用此类逻辑因为 XAML 通常调用默认构造函数之前处理属性 (集合属性或其他)。

## <a name="xaml-type-system-support-and-collections"></a>XAML 类型系统支持和集合

除了分析 XAML 和填充或序列化集合属性的基本机制，在.NET Framework XAML 服务中实现的 XAML 类型系统包括适用于 XAML 中的集合的多种设计功能。

1. <xref:System.Xaml.XamlType.IsCollection%2A> 如果 XAML 类型由提供 XAML 集合支持的类型，，返回 true。

2. <xref:System.Xaml.XamlType.IsDictionary%2A> 和<xref:System.Xaml.XamlType.IsArray%2A>可以进一步确定支持的 XAML 类型的收集模式。 对于自定义 XAML 处理器的基于.NET Framework XAML 服务和 XAML 类型系统，但不是基于现有<xref:System.Xaml.XamlWriter>实现中，了解所使用的集合模式可能需要这样才能知道要调用的方法集合处理。

3. 每个以前的属性值可能会受到的重写<xref:System.Xaml.XamlType.LookupCollectionKind%2A>XAML 类型。
