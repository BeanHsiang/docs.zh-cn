---
title: 如何：创建含调整规则的时区
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time zones [.NET Framework], creating
- time zones [.NET Framework], and adjustment rules
- adjustment rule [.NET Framework]
ms.assetid: c52ef192-13a9-435f-8015-3b12eae8c47c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 83905c97f37a0e49f6219da47e2f640ecfb8edfb
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54721170"
---
# <a name="how-to-create-time-zones-with-adjustment-rules"></a>如何：创建含调整规则的时区

应用程序所需的精确的时区信息可能不存在的特定系统上有几个原因：

* 永远不会在本地系统注册表中定义的时区。

* 有关时区的数据已修改或从注册表中删除。

* 时区没有特定的历史时期时区调整的准确信息。

在这些情况下，您可以调用<xref:System.TimeZoneInfo.CreateCustomTimeZone%2A>方法以定义你的应用程序所需的时区。 可以使用此方法的重载来创建带有或不带调整规则的时区。 如果时区支持夏令时，则可以定义与任一固定或浮动调整规则的调整。 (有关这些术语的定义，请参阅中的"时区术语"一节[时区概述](../../../docs/standard/datetime/time-zone-overview.md)。)

> [!IMPORTANT]
> 通过调用创建的自定义时区<xref:System.TimeZoneInfo.CreateCustomTimeZone%2A>方法不会添加到注册表。 相反，它们可以访问只能通过返回的对象引用<xref:System.TimeZoneInfo.CreateCustomTimeZone%2A>方法调用。

本主题演示如何创建含调整规则的时区。 若要创建不支持夏令时调整规则的时区，请参阅[如何：创建不含调整规则的时区](../../../docs/standard/datetime/create-time-zones-without-adjustment-rules.md)。

### <a name="to-create-a-time-zone-with-floating-adjustment-rules"></a>若要创建带浮动调整规则的时区

1. 对于每次调整 （即，对于每个转换离开并段特定时间间隔内回标准时间），执行以下操作：

    1. 定义时区调整的起始过渡时间。

       必须调用<xref:System.TimeZoneInfo.TransitionTime.CreateFloatingDateRule%2A?displayProperty=nameWithType>方法并将其传递<xref:System.DateTime>值，该值定义的转换、 一个整数值，定义的转换的月、 一个整数值，定义转换发生的一周的时间和<xref:System.DayOfWeek>定义在转换发生星期几的值。 此方法调用实例化<xref:System.TimeZoneInfo.TransitionTime>对象。

    2. 定义时区调整的结束转换时间。 这要求对另一个调用<xref:System.TimeZoneInfo.TransitionTime.CreateFloatingDateRule%2A?displayProperty=nameWithType>方法。 此方法调用实例化第二个<xref:System.TimeZoneInfo.TransitionTime>对象。

    3. 调用<xref:System.TimeZoneInfo.AdjustmentRule.CreateAdjustmentRule%2A>方法并将其传递的有效起始和结束日期的调整，<xref:System.TimeSpan>对象，它在转换和两个定义的时间量<xref:System.TimeZoneInfo.TransitionTime>对象，用于定义何时与夏令时的转换时间日期/时间。 此方法调用实例化<xref:System.TimeZoneInfo.AdjustmentRule>对象。

    4. 将分配<xref:System.TimeZoneInfo.AdjustmentRule>对象的数组<xref:System.TimeZoneInfo.AdjustmentRule>对象。

2. 定义时区的显示名称。 显示名称应遵循相当标准的格式时区的偏移量从协调世界时 (UTC) 括在括号中后, 跟一个字符串，标识一个或多个城市中时区，或其中一个或多个 cou 时区ntries 或时区中的区域。

3. 定义时区的标准时间的名称。 通常情况下，此字符串还用作时区的标识符。

4. 定义时区的夏时制时间的名称。

5. 如果你想要使用其他标识符，于时区的标准名称，定义的时区标识符。

6. 实例化<xref:System.TimeSpan>对象，用于定义相对于 UTC 的时区的偏移量。 时间晚于 UTC 的时区具有负偏移量。 时间早于 UTC 的时区具有负偏移量。

7. 调用<xref:System.TimeZoneInfo.CreateCustomTimeZone%28System.String%2CSystem.TimeSpan%2CSystem.String%2CSystem.String%2CSystem.String%2CSystem.TimeZoneInfo.AdjustmentRule%5B%5D%29?displayProperty=nameWithType>方法可实例化新的时区。

## <a name="example"></a>示例

下面的示例定义为包括从 1918年到最新的时间间隔的多个调整规则的美国中部标准时区。

[!code-csharp[System.TimeZone2.CreateTimeZone#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/cs/System.TimeZone2.CreateTimeZone.cs#5)]
[!code-vb[System.TimeZone2.CreateTimeZone#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/vb/System.TimeZone2.CreateTimeZone.vb#5)]

在此示例中创建的时间区域具有多个调整规则。 必须格外小心以确保有效开始日期和结束日期的任何调整规则执行不重叠的另一个调整规则的日期。 如果存在重叠，<xref:System.InvalidTimeZoneException>引发。

对于浮动调整规则，值 5 传递到`week`参数的<xref:System.TimeZoneInfo.TransitionTime.CreateFloatingDateRule%2A>方法，以指示转换发生在特定月份的最后一周。

在中创建的数组<xref:System.TimeZoneInfo.AdjustmentRule>对象中使用<xref:System.TimeZoneInfo.CreateCustomTimeZone%28System.String%2CSystem.TimeSpan%2CSystem.String%2CSystem.String%2CSystem.String%2CSystem.TimeZoneInfo.AdjustmentRule%5B%5D%29?displayProperty=nameWithType>方法调用中，该代码可以初始化到多种调整时区为创建所需的大小的数组。 相反，此代码示例调用<xref:System.Collections.Generic.List%601.Add%2A>方法将每个调整规则添加到泛型<xref:System.Collections.Generic.List%601>的集合<xref:System.TimeZoneInfo.AdjustmentRule>对象。 然后，代码调用<xref:System.Collections.Generic.List%601.CopyTo%2A>方法将此集合的成员复制到数组。

此示例还使用<xref:System.TimeZoneInfo.TransitionTime.CreateFixedDateRule%2A>方法以定义固定日期进行调整。 这是类似于调用<xref:System.TimeZoneInfo.TransitionTime.CreateFloatingDateRule%2A>方法，它需要时间、 月和日转换参数不同。

该示例可以使用类似以下的代码进行测试：

[!code-csharp[System.TimeZone2.CreateTimeZone#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/cs/System.TimeZone2.CreateTimeZone.cs#7)]
[!code-vb[System.TimeZone2.CreateTimeZone#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/vb/System.TimeZone2.CreateTimeZone.vb#7)]

## <a name="compiling-the-code"></a>编译代码

此示例需要：

* 包含对 System.Core.dll 的引用添加到项目。

* 将导入以下命名空间：

  [!code-csharp[System.TimeZone2.CreateTimeZone#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/cs/System.TimeZone2.CreateTimeZone.cs#6)]
  [!code-vb[System.TimeZone2.CreateTimeZone#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/vb/System.TimeZone2.CreateTimeZone.vb#6)]

## <a name="see-also"></a>请参阅

- [日期、时间和时区](../../../docs/standard/datetime/index.md)
- [时区概述](../../../docs/standard/datetime/time-zone-overview.md)
- [如何：创建不含调整规则的时区](../../../docs/standard/datetime/create-time-zones-without-adjustment-rules.md)
