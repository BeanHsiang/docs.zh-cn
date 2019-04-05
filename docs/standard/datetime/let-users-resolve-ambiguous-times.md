---
title: 如何：让用户解决不明确时间
ms.date: 04/10/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- time zones [.NET Framework], ambiguous time
- ambiguous time [.NET Framework]
ms.assetid: bca874ee-5b68-4654-8bbd-3711220ef332
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ae6d16bda7a2cd6f2367129b737ec79d8193ebf9
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54502710"
---
# <a name="how-to-let-users-resolve-ambiguous-times"></a>如何：让用户解决不明确时间

不明确时间是指映射到多个协调世界时 (UTC) 的时间。 在向后调整时钟时间时，例如从时区的夏令时调整到标准时间这段转换期间，便会出现不明确时间。 在处理不明确时间时，可执行以下任一操作：

* 如果不明确时间是用户输入的数据项，则可以让用户自行解决。

* 假设一下时间如何映射到 UTC。 例如，可以假定不明确时间始终以时区的标准时间表示。

本主题演示如何让用户解决不明确时间。

### <a name="to-let-a-user-resolve-an-ambiguous-time"></a>让用户解决不明确时间

1. 获取用户输入的日期和时间。

2. 调用<xref:System.TimeZoneInfo.IsAmbiguousTime%2A>方法，以确定时间是否不明确。

3. 如果时间不明确，则调用<xref:System.TimeZoneInfo.GetAmbiguousTimeOffsets%2A>方法来检索其中的数组<xref:System.TimeSpan>对象。 数组中的每个元素包含不明确时间可以映射到的 UTC 偏移量。

4. 让用户选择所需时差。

5. 用本地时间减去用户所选时差，得出 UTC 日期和时间。

6. 调用`static`(`Shared`在 Visual Basic.NET)<xref:System.DateTime.SpecifyKind%2A>方法设置的 UTC 日期和时间值的<xref:System.DateTime.Kind%2A>属性设置为<xref:System.DateTimeKind.Utc?displayProperty=nameWithType>。

## <a name="example"></a>示例

以下示例将提示用户输入日期和时间，如果时间不明确，会让用户选择不明确时间映射到的 UTC 时间。

[!code-csharp[System.TimeZone2.Concepts#11](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#11)]
[!code-vb[System.TimeZone2.Concepts#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#11)]

示例代码的核心使用一组<xref:System.TimeSpan>对象，来指示可能不明确时间与 UTC 的时差。 但是，这些时差值对用户可能没有什么意义。 为了阐明时差的含义，该代码还会指示时差是表示本地时区的标准时间还是其夏令时。 该代码将确定哪个是标准时间，哪个是夏令时进行比较的值的偏移量<xref:System.TimeZoneInfo.BaseUtcOffset%2A>属性。 此属性指示 UTC 与时区的标准时间之差。

在此示例中，对本地时区的所有引用都都通过<xref:System.TimeZoneInfo.Local%2A?displayProperty=nameWithType>属性; 区域永远不会分配给对象变量的本地时间。 这是建议的做法，因为调用<xref:System.TimeZoneInfo.ClearCachedData%2A?displayProperty=nameWithType>方法使本地时区分配给任何对象无效。

## <a name="compiling-the-code"></a>编译代码

此示例需要：

* 包含对 System.Core.dll 的引用添加到项目。

* 是否<xref:System>命名空间导入与`using`语句 （C# 代码中需要）。

## <a name="see-also"></a>请参阅

- [日期、时间和时区](../../../docs/standard/datetime/index.md)
- [如何：解决不明确时间](../../../docs/standard/datetime/resolve-ambiguous-times.md)
