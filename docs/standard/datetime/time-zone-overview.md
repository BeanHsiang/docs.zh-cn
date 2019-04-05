---
title: 时区概述
ms.date: 04/10/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- time zones [.NET Framework], about time zones
- transition time [.NET Framework]
- TimeZoneInfo class, about TimeZoneInfo class
- time zones [.NET Framework], creating
- invalid time [.NET Framework]
- fixed rule [.NET Framework]
- ambiguous time [.NET Framework]
- floating rule [.NET Framework]
- daylight saving time [.NET Framework]
- adjustment rule [.NET Framework]
- time zones [.NET Framework], terminology
ms.assetid: c4b7ed01-5e38-4959-a3b6-ef9765d6ccf1
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e5fa4376cdb0496cfd25f4764257c4f3afbc7268
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54697044"
---
# <a name="time-zone-overview"></a>时区概述

<xref:System.TimeZoneInfo>类简化了创建时区感知应用程序。 <xref:System.TimeZone>类支持使用本地时区与协调世界时 (UTC)。 <xref:System.TimeZoneInfo>类支持这两个有关哪些信息以及任何时区在注册表中预定义这些区域。 此外可以使用<xref:System.TimeZoneInfo>来定义系统没有有关的任何信息的自定义时区。

## <a name="time-zone-essentials"></a>时区概要

时区指使用相同时间的某个地理区域。 相邻时区通常（但不总是）相差一小时。 世界上任一时区的时间都能以与协调世界时 (UTC) 之间的时差表示。

世界上许多时区都实施夏令时。 夏令时是指，在春季或初夏将时间提前一小时并在夏末或秋季将时间调回正常（或标准）时间，从而最大化地利用光照。 这种针对标准时间的来回更改就称为调整规则。

特定时区中针对夏令时的来回转换可通过固定或浮动调整规则进行定义。 固定调整规则设定一个特定日期，每年都会在此时进行夏令时来回转换。 例如，每年 10 月 25 日从夏令时转换到标准时间，这一案例就是遵循的固定调整规则。 浮动调整规则更为常见，该规则会设定在特定月特定星期的某一天进行夏令时转换。 例如，在 3 月的第三个星期日从标准时间转换到夏令时，这一案例遵循的就是浮动调整规则。

对于实施调整规则的时区而言，夏令时的来回转换会导致两种反常时间：无效时间和不明确时间。 无效时间是指，从标准时间转换到夏令时而产生的不存在的时间。 例如，如果此转换发生在特定日期的凌晨 2:00， 导致时间变为凌晨 3:00，则每次凌晨 2:00  与凌晨 2:59:99  之间的时间间隔无效。 不明确时间是指一个时区内可映射到两个不同时间的时间。 从夏令时转换到标准时间后，便会产生不明确时间。 例如，如果此转换发生在特定日期的凌晨 2:00， 导致时间变为凌晨 1:00，则每次凌晨 1:00  与凌晨 1:59:99  之间的时间间隔既可理解为标准时间，也可以是夏令时时间。

## <a name="time-zone-terminology"></a>时区术语

下表定义了使用时区和开发时区感知应用程序时常用的术语。

| 术语            | 定义 |
| --------------- | ---------- |
| 调整规则 | 用于定义何时从标准时间转换为夏令时，以及何时从夏令时转换回标准时间的规则。 每个调整规则都定义了该规则已到位的开始和结束日期 （例如，调整规则是在 1986 年 1 月 1，从到 2006 年 12 月 31 日的位置），增量 （的标准时间更改由于个应用程序所依据的时间量e 调整规则），以及有关的特定日期和时间的转换来调整期间，会出现的信息。 转换可遵循固定规则或浮动规则。 |
| 不明确时间  | 一个时区内可映射到两个不同时间的时间。 在向后调整时钟时间时，例如从时区的夏令时调整到标准时间这段转换期间，便会出现不明确时间。 例如，如果此转换发生在特定日期的凌晨 2:00， 导致时间变为凌晨 1:00，则每次凌晨 1:00  与凌晨 1:59:99  之间的时间间隔既可理解为标准时间，也可以是夏令时时间。 |
| 固定规则      | 该调整规则设定发生夏令时来回转换的特定日期。 例如，每年 10 月 25 日从夏令时转换到标准时间，这一案例就是遵循的固定调整规则。 |
| 浮动规则   | 该规则设定在特定月特定星期的某一天发生夏令时来回转换。 例如，在 3 月的第三个星期日从标准时间转换到夏令时，这一案例遵循的就是浮动调整规则。 |
| 无效时间    | 从标准时间转换到夏令时而导致产生的不存在的时间。 在向前调整时钟时间时，例如从时区的标准时间转换到夏令时这段转换期间，便会出现无效时间。 例如，如果此转换发生在特定日期的凌晨 2:00， 导致时间变为凌晨 3:00，则每次凌晨 2:00  与凌晨 2:59:99  之间的时间间隔无效。 |
| 转换时间 | 有关某一特定时区中特定时间更改（例如从夏令时更改为标准时间，或者从标准时间更改为夏令时）的信息。 |

## <a name="time-zones-and-the-timezoneinfo-class"></a>时区和 TimeZoneInfo 类

在.NET 中，<xref:System.TimeZoneInfo>对象都表示一个时区。 <xref:System.TimeZoneInfo>类包括<xref:System.TimeZoneInfo.GetAdjustmentRules%2A>方法返回的数组<xref:System.TimeZoneInfo.AdjustmentRule>对象。 此数组的每个元素提供了有关特定时间段内从夏令时的来回转换的信息。 （对于不支持夏令时的时区，该方法返回空数组。）每个<xref:System.TimeZoneInfo.AdjustmentRule>对象具有<xref:System.TimeZoneInfo.AdjustmentRule.DaylightTransitionStart%2A>和一个<xref:System.TimeZoneInfo.AdjustmentRule.DaylightTransitionEnd%2A>属性，用于定义特定日期和时间转换到和从夏时制。 <xref:System.TimeZoneInfo.TransitionTime.IsFixedDateRule%2A>属性指示该转换是固定或浮动。

.NET 依赖于 Windows 操作系统提供的、 在注册表中存储的时区信息。 由于地球的时区的数量，而不是所有的现有时区表示在注册表中。 此外，由于注册表是一个动态结构，可以添加到预定义的时区，或从中移除。 最后，注册表不一定包含历史时区数据。 例如，在 Windows XP 注册表包含只运行一时区调整组有关的数据。 Windows Vista 支持动态时区数据，这意味着一个时区可以有多个调整规则应用于特定的年的时间间隔。 但是，大多数 Windows Vista 注册表和支持夏时制中定义的时区必须只能将一个或两个预定义的调整规则。

集的依赖性<xref:System.TimeZoneInfo>类对注册表意味着，时区感知应用程序不能为某些特定时区在注册表中定义。 因此，尝试实例化某个特定时区（除了本地时区或表示 UTC 的时区）时，应使用异常处理。 它还应提供一些方法，以便让应用程序继续，则所需<xref:System.TimeZoneInfo>无法从注册表实例化对象。

处理所需的时间区域，缺少<xref:System.TimeZoneInfo>类包括<xref:System.TimeZoneInfo.CreateCustomTimeZone%2A>方法，可用于创建在注册表中找不到的自定义时区。 有关创建自定义时区的详细信息，请参阅[如何：创建不含调整规则的时区](../../../docs/standard/datetime/create-time-zones-without-adjustment-rules.md)和[如何：创建含调整规则的时区](../../../docs/standard/datetime/create-time-zones-with-adjustment-rules.md)。 此外，还可以使用<xref:System.TimeZoneInfo.ToSerializedString%2A>方法将新创建的时区转换为一个字符串，并将其保存在数据存储中 （如数据库、 文本文件、 注册表中或应用程序资源）。 然后，可以使用<xref:System.TimeZoneInfo.FromSerializedString%2A>方法将此字符串转换回<xref:System.TimeZoneInfo>对象。 有关详细信息，请参阅[如何：将时区保存到嵌入的资源](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md)和[如何：从嵌入的资源还原时区](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md)。

由于每个时区均由与 UTC 之间的基本时差表示，同时也可由与反映任何现有调整规则的 UTC 之间的时差表示，因此，可轻易将一个时区内的时间转换为另一时区的时间。 为此，<xref:System.TimeZoneInfo>对象包含多个转换方法，包括：

* <xref:System.TimeZoneInfo.ConvertTimeFromUtc%2A>它将 UTC 转换为指定的时区中的时间。

* <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A>它将在指定的时区的时间转换为 UTC。

* <xref:System.TimeZoneInfo.ConvertTime%2A>它将一个指定的时区的时间转换为另一个指定的时区中的时间。

* <xref:System.TimeZoneInfo.ConvertTimeBySystemTimeZoneId%2A>它使用时区标识符 (而不是<xref:System.TimeZoneInfo>对象) 作为参数，可将一个指定的时区的时间转换为另一个指定的时区中的时间。

有关如何在时区之间转换时间的详细信息，请参阅[在不同时区间转换时间](../../../docs/standard/datetime/converting-between-time-zones.md)。

## <a name="see-also"></a>请参阅

- [日期、时间和时区](../../../docs/standard/datetime/index.md)
