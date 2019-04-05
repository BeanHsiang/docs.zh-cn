---
title: 如何：访问预定义的 UTC 和本地时区对象
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time zones [.NET Framework], local
- predefined time zones
- UTC times, predefined
- local time zone access
- time zones [.NET Framework], retrieving
- time zones [.NET Framework], UTC
ms.assetid: 961fb70b-83f0-4dab-a042-cb5fcd817cf5
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c10c07c08a4e676cf3c84a5722814eaed85f74a9
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54658021"
---
# <a name="how-to-access-the-predefined-utc-and-local-time-zone-objects"></a>如何：访问预定义的 UTC 和本地时区对象

<xref:System.TimeZoneInfo>类提供了两个属性<xref:System.TimeZoneInfo.Utc%2A>和<xref:System.TimeZoneInfo.Local%2A>，您的代码访问权限向预定义的时区对象。 本主题介绍如何访问这些属性返回的 <xref:System.TimeZoneInfo> 对象。

### <a name="to-access-the-coordinated-universal-time-utc-timezoneinfo-object"></a>访问协调世界时 (UTC) TimeZoneInfo 对象

1. 使用`static`(`Shared`在 Visual Basic 中)<xref:System.TimeZoneInfo.Utc%2A?displayProperty=nameWithType>属性访问协调世界时。

2. 而不是将分配<xref:System.TimeZoneInfo>对象的属性返回给对象变量，继续访问协调世界时通过<xref:System.TimeZoneInfo.Utc%2A?displayProperty=nameWithType>属性。

### <a name="to-access-the-local-time-zone"></a>访问本地时区

1. 使用`static`(`Shared`在 Visual Basic 中)<xref:System.TimeZoneInfo.Local%2A?displayProperty=nameWithType>属性来访问本地系统时区。

2. 而不是将分配<xref:System.TimeZoneInfo>对象的属性返回给对象变量，继续访问本地时区通过<xref:System.TimeZoneInfo.Local%2A?displayProperty=nameWithType>属性。

## <a name="example"></a>示例

下面的代码使用 <xref:System.TimeZoneInfo.Local%2A?displayProperty=nameWithType> 和 <xref:System.TimeZoneInfo.Utc%2A?displayProperty=nameWithType> 属性转换美国和加拿大东部标准时区的时间，并将时区名称显示到控制台。

[!code-csharp[System.TimeZone2.Concepts#13](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#13)]
[!code-vb[System.TimeZone2.Concepts#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#13)]

您应始终访问通过本地时区<xref:System.TimeZoneInfo.Local%2A?displayProperty=nameWithType>属性，而不是无需分配本地时间时区分配给<xref:System.TimeZoneInfo>对象变量。 同样，应始终访问协调世界时通过<xref:System.TimeZoneInfo.Utc%2A?displayProperty=nameWithType>属性，而不是无需分配 UTC 时区分配给<xref:System.TimeZoneInfo>对象变量。 这可以防止<xref:System.TimeZoneInfo>调用而失效的对象变量<xref:System.TimeZoneInfo.ClearCachedData%2A?displayProperty=nameWithType>方法。

## <a name="compiling-the-code"></a>编译代码

此示例需要：

* 包含对 System.Core.dll 的引用添加到项目。

* 是否<xref:System>命名空间导入与`using`语句 （C# 代码中需要）。

## <a name="see-also"></a>请参阅

- [日期、时间和时区](../../../docs/standard/datetime/index.md)
- [查找本地系统上定义的时区](../../../docs/standard/datetime/finding-the-time-zones-on-local-system.md)
- [如何：实例化 TimeZoneInfo 对象](../../../docs/standard/datetime/instantiate-time-zone-info.md)
