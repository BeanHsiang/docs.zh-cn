---
title: 在 DateTime 与 DateTimeOffset 之间进行转换
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DateTime structure, converting
- time zones [.NET Framework], conversions
- UTC times, converting
- DateTimeOffset structure, converting
- converting DateTimeOffset and DateTime values
- dates [.NET Framework], converting
- converting times
- Date data type, converting
- local time conversions
ms.assetid: b605ff97-0c45-4c24-833f-4c6a3e8be64c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d4bce84d26e8f498f065c887b583e18d8ea7c786
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54651196"
---
# <a name="converting-between-datetime-and-datetimeoffset"></a>在 DateTime 与 DateTimeOffset 之间进行转换

尽管<xref:System.DateTimeOffset>结构可提供更高的比时区感知<xref:System.DateTime>结构，<xref:System.DateTime>更常见的方法调用中使用参数。 因此，要转换的功能<xref:System.DateTimeOffset>值到<xref:System.DateTime>值，反之亦然更是如此。 本主题演示如何保留尽可能多时区信息的方式执行这些转换。

> [!NOTE]
> 同时<xref:System.DateTime>和<xref:System.DateTimeOffset>类型表示时区内的时间时存在一些限制。 使用其<xref:System.DateTime.Kind%2A>属性，<xref:System.DateTime>能够反映只有协调世界时 (UTC) 和系统的本地时区。 <xref:System.DateTimeOffset> 反映了时间的 UTC 偏移量，但它不反映实际时区的偏移量所属。 时间值和时区支持的详细信息，请参阅[选择之间 DateTime、 DateTimeOffset、 TimeSpan 和 TimeZoneInfo](../../../docs/standard/datetime/choosing-between-datetime.md)。

## <a name="conversions-from-datetime-to-datetimeoffset"></a>从 DateTime 转换为 DateTimeOffset

<xref:System.DateTimeOffset>结构提供了两个等效方法来执行<xref:System.DateTime>到<xref:System.DateTimeOffset>适用于大多数转换的转换：

* <xref:System.DateTimeOffset.%23ctor%2A>构造函数，创建一个新<xref:System.DateTimeOffset>对象，基于<xref:System.DateTime>值。

* 隐式转换运算符，可用于将分配<xref:System.DateTime>值设为<xref:System.DateTimeOffset>对象。

对于 UTC 和本地<xref:System.DateTime>值，<xref:System.DateTimeOffset.Offset%2A>生成的属性<xref:System.DateTimeOffset>值准确反映 UTC 或本地时间的时区偏移量。 例如，下面的代码将 UTC 时间转换为其等效<xref:System.DateTimeOffset>值。

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#1)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#1)]

在本例中，`utcTime2` 变量的偏移量为 00:00。 同样，以下代码将本地时间转换为其等效<xref:System.DateTimeOffset>值。

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#2)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#2)]

但是，对于<xref:System.DateTime>值<xref:System.DateTime.Kind%2A>属性是<xref:System.DateTimeKind.Unspecified?displayProperty=nameWithType>，这两个转换方法生成<xref:System.DateTimeOffset>其偏移量为本地时区的值。 以下示例对此进行了演示，该示例在美国太平洋标准时区运行。

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#3)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#3)]

如果<xref:System.DateTime>值反映的日期和时间中的内容以外的本地时区或 UTC，您可以将其转换为<xref:System.DateTimeOffset>值，并通过调用重载保留其时区信息<xref:System.DateTimeOffset.%23ctor%2A>构造函数。 例如，下面的示例实例化<xref:System.DateTimeOffset>反映中部标准时间的对象。

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#4)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#4)]

此构造函数重载，第二个参数<xref:System.TimeSpan>对象，它表示时间的偏移量相对于 UTC，应通过调用检索<xref:System.TimeZoneInfo.GetUtcOffset%28System.DateTime%29?displayProperty=nameWithType>方法的相应的时间的时区。 该方法的单个参数是<xref:System.DateTime>值，该值表示要转换的日期和时间。 如果时区支持夏令时，此参数允许方法为该特定日期和时间确定适当偏移量。

## <a name="conversions-from-datetimeoffset-to-datetime"></a>从 DateTimeOffset 转换为 DateTime

<xref:System.DateTimeOffset.DateTime%2A>属性最常用于执行<xref:System.DateTimeOffset>到<xref:System.DateTime>转换。 但是，它将返回<xref:System.DateTime>值，其<xref:System.DateTime.Kind%2A>属性是<xref:System.DateTimeKind.Unspecified>，如下面的示例所示。

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#5)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#5)]

这意味着，任何信息有关<xref:System.DateTimeOffset>转换为 UTC 值的关系会丢失时<xref:System.DateTimeOffset.DateTime%2A>使用属性。 这会影响<xref:System.DateTimeOffset>这些值对应于 UTC 时间或系统的本地时间，因为<xref:System.DateTimeOffset.DateTime%2A>结构反映了仅这两个时区中其<xref:System.DateTime.Kind%2A>属性。

若要在转换时保留尽可能多的时区信息可能<xref:System.DateTimeOffset>到<xref:System.DateTime>值，则可以使用<xref:System.DateTimeOffset.UtcDateTime%2A?displayProperty=nameWithType>和<xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=nameWithType>属性。

### <a name="converting-a-utc-time"></a>转换 UTC 时间

若要指示转换后<xref:System.DateTimeOffset.DateTime%2A>值是 UTC 时间，可以检索的值<xref:System.DateTimeOffset.UtcDateTime%2A?displayProperty=nameWithType>属性。 它不同于<xref:System.DateTimeOffset.DateTime%2A>两种方式的属性：

* 它将返回<xref:System.DateTime>值，其<xref:System.DateTime.Kind%2A>属性是<xref:System.DateTimeKind.Utc>。

* 如果<xref:System.DateTimeOffset.Offset%2A>属性值不等于<xref:System.TimeSpan.Zero?displayProperty=nameWithType>，它将时间转换为 UTC。

> [!NOTE]
> 如果你的应用程序需要已转换<xref:System.DateTime>值明确标识单个点的时间，则应考虑使用<xref:System.DateTimeOffset.UtcDateTime%2A?displayProperty=nameWithType>属性来处理所有<xref:System.DateTimeOffset>到<xref:System.DateTime>转换。

下面的代码使用<xref:System.DateTimeOffset.UtcDateTime%2A>属性来转换<xref:System.DateTimeOffset>值，其偏移量等于<xref:System.TimeSpan.Zero?displayProperty=nameWithType>到<xref:System.DateTime>值。

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#6)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#6)]

下面的代码使用<xref:System.DateTimeOffset.UtcDateTime%2A>属性上执行时区转换和类型转换<xref:System.DateTimeOffset>值。

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#12](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#12)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#12)]

### <a name="converting-a-local-time"></a>转换本地时间

若要指示<xref:System.DateTimeOffset>值表示本地时间，则可以通过<xref:System.DateTime>返回的值<xref:System.DateTimeOffset.DateTime%2A?displayProperty=nameWithType>属性设置为`static`(`Shared` Visual Basic 中)<xref:System.DateTime.SpecifyKind%2A>方法。 该方法返回的日期和时间作为其第一个参数传递给它，但设置<xref:System.DateTime.Kind%2A>属性设置为第二个参数指定的值。 下面的代码使用<xref:System.DateTime.SpecifyKind%2A>方法转换时<xref:System.DateTimeOffset>值其偏移量对应于本地时区。

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#7)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#7)]

此外可以使用<xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=nameWithType>属性来转换<xref:System.DateTimeOffset>值到本地<xref:System.DateTime>值。 <xref:System.DateTime.Kind%2A>所返回的属性<xref:System.DateTime>值是<xref:System.DateTimeKind.Local>。 下面的代码使用<xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=nameWithType>属性将转换时<xref:System.DateTimeOffset>值其偏移量对应于本地时区。 

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#10](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#10)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#10)]

当检索<xref:System.DateTime>值使用<xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=nameWithType>属性，该属性的`get`访问器首先将转换<xref:System.DateTimeOffset>值为 UTC，然后将其转换为本地时间通过调用<xref:System.DateTimeOffset.ToLocalTime%2A>方法。 这意味着您可以检索从值<xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=nameWithType>属性执行时区转换同时执行类型转换。 还意味着在执行转换期间应用本地时区的调整规则。 下面的代码演示如何使用<xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=nameWithType>属性来执行类型和时区转换。

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#11](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#11)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#11)]

### <a name="a-general-purpose-conversion-method"></a>通用转换方法

下面的示例定义一个名为方法`ConvertFromDateTimeOffset`，用于将<xref:System.DateTimeOffset>值到<xref:System.DateTime>值。 根据其偏移量，它确定是否<xref:System.DateTimeOffset>值是 UTC 时间、 本地时间还是其他时间，并定义返回的日期和时间值的<xref:System.DateTime.Kind%2A>属性相应地。

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#8](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#8)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#8)]

下面的示例调用`ConvertFromDateTimeOffset`方法将<xref:System.DateTimeOffset>表示 UTC 时间、 本地时间和美国中的某个时间的值中部标准时区的时间。

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#9](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#9)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#9)]

请注意，此代码根据应用程序及其日期和时间值的来源所作的两种假设不一定始终有效：

* 它假定的日期和时间值的偏移量是<xref:System.TimeSpan.Zero?displayProperty=nameWithType>表示 UTC。 事实上，UTC 并不是特定时区中的时间，而是世界时区中的时间相对于它进行标准化的时间。 时区还具有偏移量为<xref:System.TimeSpan.Zero>。

* 假定偏移量等于本地时区偏移量的日期和时间表示本地时区。 由于日期和时间值已从其原始时区解除关联，因此这可能不成立；日期和时间可能源自具有相同偏移量的其他时区。

## <a name="see-also"></a>请参阅

- [日期、时间和时区](../../../docs/standard/datetime/index.md)
