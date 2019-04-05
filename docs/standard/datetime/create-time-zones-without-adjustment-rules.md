---
title: 如何：创建不含调整规则的时区
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time zones [.NET Framework], adjustment rule
- time zones [.NET Framework], creating
- adjustment rule [.NET Framework]
ms.assetid: a6af8647-7893-4f29-95a9-d94c65a6e8dd
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: cb3ffc7b6f1f7baec7ce6beb5a50b706ff78bfa1
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54681711"
---
# <a name="how-to-create-time-zones-without-adjustment-rules"></a>如何：创建不含调整规则的时区

应用程序所需的精确的时区信息可能不存在的特定系统上有几个原因：

* 永远不会在本地系统注册表中定义的时区。

* 有关时区的数据已修改或从注册表中删除。

* 时区存在，但不具有特定的历史时期时区调整的准确信息。

在这些情况下，您可以调用<xref:System.TimeZoneInfo.CreateCustomTimeZone%2A>方法以定义你的应用程序所需的时区。 可以使用此方法的重载来创建带有或不带调整规则的时区。 如果时区支持夏令时，则可以定义与任一固定或浮动调整规则的调整。 (有关这些术语的定义，请参阅中的"时区术语"一节[时区概述](../../../docs/standard/datetime/time-zone-overview.md)。)

> [!IMPORTANT]
> 通过调用创建的自定义时区<xref:System.TimeZoneInfo.CreateCustomTimeZone%2A>方法不会添加到注册表。 相反，它们可以访问只能通过返回的对象引用<xref:System.TimeZoneInfo.CreateCustomTimeZone%2A>方法调用。

本主题演示如何创建不含调整规则的时区。 若要创建支持夏令时调整规则的时区，请参阅[如何：创建含调整规则的时区](../../../docs/standard/datetime/create-time-zones-with-adjustment-rules.md)。

### <a name="to-create-a-time-zone-without-adjustment-rules"></a>若要创建不含调整规则的时区

1. 定义时区的显示名称。

   显示名称应遵循相当标准的格式时区的偏移量从协调世界时 (UTC) 括在括号中后, 跟一个字符串，标识一个或多个城市中时区，或其中一个或多个 cou 时区ntries 或时区中的区域。

2. 定义时区的标准时间的名称。 通常情况下，此字符串还用作时区的标识符。

3. 如果你想要使用其他标识符，于时区的标准名称，定义的时区标识符。

4. 实例化<xref:System.TimeSpan>对象，用于定义相对于 UTC 的时区的偏移量。 时间晚于 UTC 的时区具有负偏移量。 时间早于 UTC 的时区具有负偏移量。

5. 调用<xref:System.TimeZoneInfo.CreateCustomTimeZone%28System.String%2CSystem.TimeSpan%2CSystem.String%2CSystem.String%29?displayProperty=nameWithType>方法可实例化新的时区。

## <a name="example"></a>示例

下面的示例定义莫森，南极洲，带调整规则的自定义时区。

[!code-csharp[System.TimeZone2.CreateTimeZone#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/cs/System.TimeZone2.CreateTimeZone.cs#1)]
[!code-vb[System.TimeZone2.CreateTimeZone#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/vb/System.TimeZone2.CreateTimeZone.vb#1)]

将字符串分配给<xref:System.TimeZoneInfo.DisplayName%2A>属性应遵循标准格式，相对于 UTC 的时区的偏移量跟时区的易懂说明。

## <a name="compiling-the-code"></a>编译代码

此示例需要：

* 包含对 System.Core.dll 的引用添加到项目。

* 将导入以下命名空间：

  [!code-csharp[System.TimeZone2.CreateTimeZone#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/cs/System.TimeZone2.CreateTimeZone.cs#6)]
  [!code-vb[System.TimeZone2.CreateTimeZone#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/vb/System.TimeZone2.CreateTimeZone.vb#6)]

## <a name="see-also"></a>请参阅

- [日期、时间和时区](../../../docs/standard/datetime/index.md)
- [时区概述](../../../docs/standard/datetime/time-zone-overview.md)
- [如何：创建含调整规则的时区](../../../docs/standard/datetime/create-time-zones-with-adjustment-rules.md)
