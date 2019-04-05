---
title: 保存和还原时区
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- restoring time zones
- deserialization [.NET Framework], time zones
- serialization [.NET Framework], time zones
- time zone objects [.NET Framework], restoring
- saving time zones
- time zone objects [.NET Framework], deserializing
- time zones [.NET Framework], saving
- time zones [.NET Framework], restoring
- time zone objects [.NET Framework], serializing
- time zone objects [.NET Framework], saving
ms.assetid: 4028b310-e7ce-49d4-a646-1e83bfaf6f9d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9d783f9e0d098e472dcf67aea394804d6eef2662
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54569450"
---
# <a name="saving-and-restoring-time-zones"></a>保存和还原时区

<xref:System.TimeZoneInfo>类依赖于注册表以检索预定义的时区数据。 但是，注册表是一个动态结构。 此外，操作系统使用的注册表包含时区信息主要用于当前年度的处理时间调整和转换。 这样做有两个主要影响的应用程序依赖于准确的时区数据：

* 不能在注册表中，定义应用程序所需的时区或它可能已重命名或从注册表中删除。

* 在注册表中定义的时区可能缺少所需的历史时区转换的特定的调整规则有关的信息。

<xref:System.TimeZoneInfo>类解决了这些限制通过其支持 （保存） 的序列化和反序列化 （还原） 的时区数据。

## <a name="time-zone-serialization-and-deserialization"></a>时区序列化和反序列化

保存和还原时区由序列化和反序列化时区数据涉及两个方法调用：

* 可以序列化<xref:System.TimeZoneInfo>对象通过调用该对象的<xref:System.TimeZoneInfo.ToSerializedString%2A>方法。 该方法不带任何参数，并返回一个字符串，包含时区信息。

* 可以反序列化<xref:System.TimeZoneInfo>中通过将传递到该字符串序列化字符串对象`static`(`Shared`在 Visual Basic 中)<xref:System.TimeZoneInfo.FromSerializedString%2A?displayProperty=nameWithType>方法。

## <a name="serialization-and-deserialization-scenarios"></a>序列化和反序列化方案

保存 （或序列化） 的功能<xref:System.TimeZoneInfo>对象，为字符串以及还原 （或反序列化） 它以供将来使用会增加该实用工具和灵活性<xref:System.TimeZoneInfo>类。 本部分介绍一些序列化和反序列化是最有用的情况。

### <a name="serializing-and-deserializing-time-zone-data-in-an-application"></a>序列化和反序列化的应用程序中的时区数据

在需要时，可以从字符串还原序列化的时区。 如果从注册表检索时区不能正确地转换日期和时间在特定日期范围内的，应用程序可以这样做。 例如，Windows XP 注册表中的时区数据支持一个调整规则，而通常在 Windows Vista 注册表中定义的时区提供信息如何通过两个调整规则。 这意味着历史时间转换可能不准确。 序列化和反序列化的时区数据可以处理此限制。

在下面的示例中，自定义<xref:System.TimeZoneInfo>带调整规则的类定义来表示美国的美国东部标准时区从 1883年到 1917 夏时制在美国，引入之前。 自定义时区进行序列化具有全局作用域的变量中。 时区转换方法， `ConvertUtcTime`，传递协调通用时 (UTC) 时间转换。 如果日期和时间发生在 1917 年或更早版本，自定义的东部标准时区还原从序列化的字符串，并替换从注册表检索的时区。

[!code-csharp[System.TimeZone2.Serialization.1#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Serialization.1/cs/Serialization.cs#1)]
[!code-vb[System.TimeZone2.Serialization.1#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Serialization.1/vb/Serialization.vb#1)]

### <a name="handling-time-zone-exceptions"></a>处理时区异常

因为注册表是一个动态结构，其内容可能会发生意外或有意的修改。 这意味着可能不存在时区，应在注册表中定义和所需的应用程序才能成功执行。 不支持时区序列化和反序列化，则只能选择但若要处理生成<xref:System.TimeZoneNotFoundException>通过结束应用程序。 但是，通过使用时区序列化和反序列化，您可以处理了意外<xref:System.TimeZoneNotFoundException>通过还原从序列化的字符串和应用程序所需的时区将继续运行。

下面的示例创建并序列化自定义的中部标准时区。 然后，它尝试从注册表检索中部标准时区。 如果检索操作引发任一<xref:System.TimeZoneNotFoundException>或<xref:System.InvalidTimeZoneException>，异常处理程序反序列化时区。

[!code-csharp[System.TimeZone2.Serialization.2#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Serialization.2/cs/Serialization2.cs#1)]
[!code-vb[System.TimeZone2.Serialization.2#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Serialization.2/vb/Serialization2.vb#1)]

### <a name="storing-a-serialized-string-and-restoring-it-when-needed"></a>存储序列化的字符串并将其在需要时还原

前面的示例包含存储到字符串变量的时区信息且已在需要时还原。 但是，包含区域信息可以本身存储在某种存储介质，如外部文件，资源文件的序列化的时间字符串嵌入到应用程序或注册表中。 （请注意，应在注册表中的系统的时区项除了存储有关的自定义时区的信息。）

在这种方式中存储的序列化的时区字符串也是将时区创建例程与应用程序本身分隔开来。 例如，时区创建例程可以执行，并创建包含应用程序可以使用历史时区信息的数据文件。 数据文件可以是，则安装应用程序中，可以打开该文件和一个或多个其时间区域可以反序列化应用程序需要它们时。

使用嵌入的资源来存储序列化的时区数据的示例，请参阅[如何：将时区保存到嵌入的资源](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md)和[如何：从嵌入的资源还原时区](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md)。

## <a name="see-also"></a>请参阅

- [日期、时间和时区](../../../docs/standard/datetime/index.md)
