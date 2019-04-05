---
title: 实例化 DateTimeOffset 对象
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- instantiating time zone objects
- time zone objects [.NET Framework], instantiation
- DateTimeOffset structure, converting to DateTime
- DateTimeOffset structure, instantiating
ms.assetid: 9648375f-d368-4373-a976-3332ece00c0a
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 11f62b8fe8a28d6fe6401d53dac4b9bc1c45b21d
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54554592"
---
# <a name="instantiating-a-datetimeoffset-object"></a>实例化 DateTimeOffset 对象

<xref:System.DateTimeOffset> 结构提供了多种创建新 <xref:System.DateTimeOffset> 值的方法。 其中的许多直接对应于实例化新的可用方法<xref:System.DateTime>值，包含允许您指定的日期和时间值的偏移量从协调世界时 (UTC) 的增强功能。 具体而言，您可以实例化<xref:System.DateTimeOffset>值按以下方式：

* 通过使用日期和时间文字。

* 通过调用<xref:System.DateTimeOffset>构造函数。

* 通过隐式转换到的值<xref:System.DateTimeOffset>值。

* 分析日期和时间的字符串表示形式。

本主题提供了更高版本的详细信息和代码示例，展示了这些方法的实例化新<xref:System.DateTimeOffset>值。

## <a name="date-and-time-literals"></a>日期和时间文本

语言的支持，实例化的最常见方式之一<xref:System.DateTime>值是提供的日期和时间作为硬编码文本值。 例如，以下 Visual Basic 代码创建<xref:System.DateTime>对象，其值是 2008 年 1 月 1 日，上午 10:00。

[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#1)]

<xref:System.DateTimeOffset> 此外可以使用支持的语言时使用日期和时间文本初始化值<xref:System.DateTime>原义字符。 例如，以下 Visual Basic 代码创建<xref:System.DateTimeOffset>对象。

[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#2)]

如控制台输出所示，<xref:System.DateTimeOffset>以这种方式创建的值分配的本地时区偏移量。 这意味着，<xref:System.DateTimeOffset>分配使用的字符文本值不会标识单个时间点的代码运行不同的计算机上。

## <a name="datetimeoffset-constructors"></a>DateTimeOffset 构造函数

<xref:System.DateTimeOffset>类型定义了六个构造函数。 其中四个直接对应<xref:System.DateTime>带有类型的其他参数的构造函数<xref:System.TimeSpan>定义日期和时间的 UTC 偏移量。 这些规则可以定义<xref:System.DateTimeOffset>值基于其单独的日期和时间组件的值。 例如，以下代码使用以下四个构造函数实例化<xref:System.DateTimeOffset>对象具有相同的值，2008 年 7 月 1 日的上午 12:05 + 01:00。

[!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#3)]
[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#3)]

请注意，当的值<xref:System.DateTimeOffset>对象实例化使用<xref:System.Globalization.PersianCalendar>对象作为其构造函数的自变量之一显示到控制台，它将表示为公历而不是波斯历的日期。 若要输出使用波斯历的日期，请参阅中的示例<xref:System.Globalization.PersianCalendar>主题。

其他两个构造函数创建<xref:System.DateTimeOffset>对象从<xref:System.DateTime>值。 其中第一个具有一个参数，<xref:System.DateTime>值将转换为<xref:System.DateTimeOffset>值。 所生成的偏移量<xref:System.DateTimeOffset>值取决于<xref:System.DateTime.Kind%2A>构造函数的单个参数的属性。 如果其值为<xref:System.DateTimeKind.Utc?displayProperty=nameWithType>，偏移量设置为等于<xref:System.TimeSpan.Zero?displayProperty=nameWithType>。 否则，会将其时差设置为等于本地时区的时差。 下面的示例演示如何使用此构造函数实例化<xref:System.DateTimeOffset>表示 UTC 和本地时区对象：

[!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#4)]
[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#4)]

> [!NOTE]
> 调用的重载<xref:System.DateTimeOffset>构造函数具有单个<xref:System.DateTime>参数等效于执行的隐式转换<xref:System.DateTime>值设为<xref:System.DateTimeOffset>值。

创建第二个构造函数<xref:System.DateTimeOffset>对象从<xref:System.DateTime>值具有两个参数：<xref:System.DateTime>要转换值，和一个<xref:System.TimeSpan>值，该值表示的日期和时间的 UTC 偏移量。 此偏移量的值必须对应于<xref:System.DateTime.Kind%2A>构造函数的第一个参数的属性或<xref:System.ArgumentException>引发。 如果<xref:System.DateTime.Kind%2A>属性的第一个参数是<xref:System.DateTimeKind.Utc?displayProperty=nameWithType>，第二个参数的值必须为<xref:System.TimeSpan.Zero?displayProperty=nameWithType>。 如果<xref:System.DateTime.Kind%2A>属性的第一个参数是<xref:System.DateTimeKind.Local?displayProperty=nameWithType>，第二个参数的值必须是本地系统时区的偏移量。 如果<xref:System.DateTime.Kind%2A>属性的第一个参数是<xref:System.DateTimeKind.Unspecified?displayProperty=nameWithType>，那么时差可以是任何有效的值。 下面的代码演示如何调用此构造函数将转换<xref:System.DateTime>到<xref:System.DateTimeOffset>值。

[!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#5)]
[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#5)]

## <a name="implicit-type-conversion"></a>隐式类型转换

<xref:System.DateTimeOffset>类型支持一次隐式类型转换： 从<xref:System.DateTime>值设为<xref:System.DateTimeOffset>值。 隐式类型转换是指从一种类型转换为另一种类型，而无需显示转换（通过 C# 或 Visual Basic）且不会丢失信息。 它可以实现如下代码。

[!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#6)]
[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#6)]

所生成的偏移量<xref:System.DateTimeOffset>值取决于<xref:System.DateTime.Kind%2A?displayProperty=nameWithType>属性值。 如果其值为<xref:System.DateTimeKind.Utc?displayProperty=nameWithType>，偏移量设置为等于<xref:System.TimeSpan.Zero?displayProperty=nameWithType>。 如果其值为<xref:System.DateTimeKind.Local?displayProperty=nameWithType>或<xref:System.DateTimeKind.Unspecified?displayProperty=nameWithType>，偏移量设置为等于本地时区。

## <a name="parsing-the-string-representation-of-a-date-and-time"></a>分析日期和时间的字符串表示形式

<xref:System.DateTimeOffset>类型支持四种方法，可用于转换的字符串表示形式的日期和时间入<xref:System.DateTimeOffset>值：

* <xref:System.DateTimeOffset.Parse%2A>它尝试将转换的字符串表示形式的日期和时间为<xref:System.DateTimeOffset>值则会引发异常，如果转换失败。

* <xref:System.DateTimeOffset.TryParse%2A>它尝试将转换的字符串表示形式的日期和时间为<xref:System.DateTimeOffset>值并返回`false`如果转换失败。

* <xref:System.DateTimeOffset.ParseExact%2A>尝试将日期和时间的指定格式的字符串表示形式转换<xref:System.DateTimeOffset>值。 如果转换失败，该方法将引发异常。

* <xref:System.DateTimeOffset.TryParseExact%2A>尝试将日期和时间的指定格式的字符串表示形式转换<xref:System.DateTimeOffset>值。 如果转换失败，该方法将返回 `false`。

下面的示例演示对每个四个字符串转换方法的调用来实例化<xref:System.DateTimeOffset>值。

[!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#7)]
[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#7)]

## <a name="see-also"></a>请参阅

- [日期、时间和时区](../../../docs/standard/datetime/index.md)
