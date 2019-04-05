---
title: 如何：将时区保存到嵌入的资源
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time zones [.NET Framework], saving
- time zone objects [.NET Framework], serializing
- time zone objects [.NET Framework], saving
ms.assetid: 3c96d83a-a057-4496-abb0-8f4b12712558
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c67a97193d186275e6a788f6b18bbc17c535f367
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54592869"
---
# <a name="how-to-save-time-zones-to-an-embedded-resource"></a>如何：将时区保存到嵌入的资源

时区感知应用程序通常需要某个特定时区存在。 但是，因为单个可用性<xref:System.TimeZoneInfo>对象取决于存储在本地系统注册表中的信息，即使通常可用的时区可能不存在。 此外，有关自定义时区的信息通过使用实例化<xref:System.TimeZoneInfo.CreateCustomTimeZone%2A>方法不会存储在注册表中其他时区信息。 若要确保这些时间区域可在需要时，可以通过序列化，将其保存，并更高版本进行反序列化这些还原它们。

通常情况下，序列化<xref:System.TimeZoneInfo>对象出现除了时区感知应用程序。 具体取决于用来保存序列化数据存储<xref:System.TimeZoneInfo>对象所在的时区数据可能会进行序列化 （例如，当数据存储在注册表的应用程序密钥），设置或安装例程的一部分或作为运行实用程序例程的一部分之前在最终应用程序 （例如，当序列化的数据存储在.NET XML 资源 (.resx) 文件） 编译。

与应用程序编译的资源文件，除了几个其他数据存储可以用于时区信息。 其中包括：

* 在注册表中。 请注意应用程序应使用其自己的应用程序项的子项来存储自定义时区数据，而不是使用 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones 的子项。

* 配置文件。

* 其他系统文件。

### <a name="to-save-a-time-zone-by-serializing-it-to-a-resx-file"></a>若要通过序列化到.resx 文件中保存时区

1. 检索现有的时区，或者创建新的时区。

   若要检索现有的时区，请参阅[如何：访问预定义的 UTC 和本地时区对象](../../../docs/standard/datetime/access-utc-and-local.md)和[如何：实例化 TimeZoneInfo 对象](../../../docs/standard/datetime/instantiate-time-zone-info.md)。

   若要创建新的时区，请调用的重载之一<xref:System.TimeZoneInfo.CreateCustomTimeZone%2A>方法。 有关详细信息，请参阅[如何：创建不含调整规则的时区](../../../docs/standard/datetime/create-time-zones-without-adjustment-rules.md)和[如何：创建含调整规则的时区](../../../docs/standard/datetime/create-time-zones-with-adjustment-rules.md)。

2. 调用<xref:System.TimeZoneInfo.ToSerializedString%2A>方法来创建包含时区的数据的字符串。

3. 实例化<xref:System.IO.StreamWriter>对象提供名称和 （可选） 的.resx 文件的路径<xref:System.IO.StreamWriter>类构造函数。

4. 实例化<xref:System.Resources.ResXResourceWriter>对象通过传递<xref:System.IO.StreamWriter>对象传递给<xref:System.Resources.ResXResourceWriter>类构造函数。

5. Pass 时区的序列化到字符串<xref:System.Resources.ResXResourceWriter.AddResource%2A?displayProperty=nameWithType>方法。

6. 调用 <xref:System.Resources.ResXResourceWriter.Generate%2A?displayProperty=nameWithType> 方法。

7. 调用 <xref:System.Resources.ResXResourceWriter.Close%2A?displayProperty=nameWithType> 方法。

8. 关闭<xref:System.IO.StreamWriter>对象通过调用其<xref:System.IO.StreamWriter.Close%2A>方法。

9. 将生成的.resx 文件添加到应用程序的 Visual Studio 项目。

10. 使用**属性**窗口在 Visual Studio 中，请确保.resx 文件**生成操作**属性设置为**嵌入的资源**。

## <a name="example"></a>示例

下面的示例序列化为<xref:System.TimeZoneInfo>对象，表示中部标准时间和<xref:System.TimeZoneInfo>表示帕默站，南极时间名为 SerializedTimeZones.resx.NET XML 资源文件的对象。 在注册表中; 通常定义中部标准时间帕默站，南极是自定义时区。

[!code-csharp[TimeZone2.Serialization#1](../../../samples/snippets/csharp/VS_Snippets_CLR/TimeZone2.Serialization/cs/SerializeTimeZoneData.cs#1)]
[!code-vb[TimeZone2.Serialization#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/TimeZone2.Serialization/vb/SerializeTimeZoneData.vb#1)]

此示例中序列化<xref:System.TimeZoneInfo>对象，使他们能够在资源文件在编译时。

因为<xref:System.Resources.ResXResourceWriter.Generate%2A?displayProperty=nameWithType>方法将完整的标头信息添加到.NET XML 资源文件，所以不能用来将资源添加到现有文件。 通过检查 SerializedTimeZones.resx 文件，该示例处理这和，如果存在，而不存储所有其资源的两个序列化时区为泛型<xref:System.Collections.Generic.Dictionary%602>对象。 然后删除现有文件和现有的资源添加到新的 SerializedTimeZones.resx 文件。 序列化的时区数据也添加到此文件。

密钥 (或**名称**) 的资源的字段不应包含嵌入的空格。 <xref:System.String.Replace%28System.String%2CSystem.String%29>调用方法之前分配给资源文件所在的时区标识符中删除所有嵌入的空格。

## <a name="compiling-the-code"></a>编译代码

此示例需要：

* 对 system.windows.forms.dll 的引用和 System.Core.dll 的引用将添加到项目。

* 将导入以下命名空间：

  [!code-csharp[TimeZone2.Serialization#2](../../../samples/snippets/csharp/VS_Snippets_CLR/TimeZone2.Serialization/cs/SerializeTimeZoneData.cs#2)]
  [!code-vb[TimeZone2.Serialization#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/TimeZone2.Serialization/vb/SerializeTimeZoneData.vb#2)]

## <a name="see-also"></a>请参阅

- [日期、时间和时区](../../../docs/standard/datetime/index.md)
- [时区概述](../../../docs/standard/datetime/time-zone-overview.md)
- [如何：从嵌入的资源还原时区](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md)
