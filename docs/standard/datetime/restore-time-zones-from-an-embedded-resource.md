---
title: 如何：从嵌入的资源还原时区
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time zones [.NET Framework], deserializing
- time zones [.NET Framework], restoring
ms.assetid: 6b7b4de9-da07-47e3-8f4c-823f81798ee7
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 71fc4e04c87dfa3b83eabb06361d1da94a512a5e
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54656799"
---
# <a name="how-to-restore-time-zones-from-an-embedded-resource"></a>如何：从嵌入的资源还原时区

本主题介绍如何还原已保存的资源文件中的时区。 有关信息和有关保存时区的说明，请参阅[如何：将时区保存到嵌入的资源](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md)。

### <a name="to-deserialize-a-timezoneinfo-object-from-an-embedded-resource"></a>要反序列化 TimeZoneInfo 对象从嵌入的资源

1. 如果要检索时区不是自定义时区，请尝试使用来实例化它<xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A>方法。

2. 实例化<xref:System.Resources.ResourceManager>通过将嵌入的资源文件和对包含资源文件的程序集的引用的完全限定的名称传递的对象。

   如果您不能确定嵌入的资源文件的完全限定的名称，请使用[Ildasm.exe （IL 反汇编程序）](../../../docs/framework/tools/ildasm-exe-il-disassembler.md)来检查程序集的清单。 `.mresource`条目标识的资源。 在示例中，资源的完全限定的名称是`SerializeTimeZoneData.SerializedTimeZones`。

   如果包含时区实例化代码在同一程序集中嵌入资源文件，可以通过调用来检索对它的引用`static`(`Shared`在 Visual Basic 中)<xref:System.Reflection.Assembly.GetExecutingAssembly%2A>方法。

3. 如果在调用<xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A>方法失败，或如果要实例化自定义时区，检索一个字符串，通过调用包含序列化的时区<xref:System.Resources.ResourceManager.GetString%2A?displayProperty=nameWithType>方法。

4. 通过调用所在的时区数据反序列化<xref:System.TimeZoneInfo.FromSerializedString%2A>方法。

## <a name="example"></a>示例

下面的示例进行反序列化<xref:System.TimeZoneInfo>嵌入.NET XML 资源文件中存储对象。

[!code-csharp[TimeZone2.Serialization#3](../../../samples/snippets/csharp/VS_Snippets_CLR/TimeZone2.Serialization/cs/SerializeTimeZoneData.cs#3)]
[!code-vb[TimeZone2.Serialization#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/TimeZone2.Serialization/vb/SerializeTimeZoneData.vb#3)]

以下代码说明了异常处理，以确保<xref:System.TimeZoneInfo>应用程序所需的对象是否存在。 它首先尝试实例化<xref:System.TimeZoneInfo>通过从注册表中使用检索的对象<xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A>方法。 如果不能实例化时区，代码会检索它从嵌入的资源文件。

因为自定义时区的数据 (通过使用实例化时区<xref:System.TimeZoneInfo.CreateCustomTimeZone%2A>方法) 不存储在注册表中，代码不调用<xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A>帕默南极洲实例化时区。 相反，它立即查找到嵌入的资源文件，以检索一个字符串，包含时区的数据，调用之前<xref:System.TimeZoneInfo.FromSerializedString%2A>方法。

## <a name="compiling-the-code"></a>编译代码

此示例需要：

* 对 system.windows.forms.dll 的引用和 System.Core.dll 的引用将添加到项目。

* 将导入以下命名空间：

  [!code-csharp[TimeZone2.Serialization#2](../../../samples/snippets/csharp/VS_Snippets_CLR/TimeZone2.Serialization/cs/SerializeTimeZoneData.cs#2)]
  [!code-vb[TimeZone2.Serialization#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/TimeZone2.Serialization/vb/SerializeTimeZoneData.vb#2)]

## <a name="see-also"></a>请参阅

- [日期、时间和时区](../../../docs/standard/datetime/index.md)
- [时区概述](../../../docs/standard/datetime/time-zone-overview.md)
- [如何：将时区保存到嵌入的资源](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md)
