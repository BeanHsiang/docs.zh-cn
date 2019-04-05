---
title: 如何：枚举计算机上存在的时区
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time zones [.NET Framework], enumerating
- enumerating time zones [.NET Framework]
ms.assetid: bb7a42ab-6bd9-4c5c-b734-5546d51f8669
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 697cd40482aee73fd150359acb710ffc258c3df2
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54518405"
---
# <a name="how-to-enumerate-time-zones-present-on-a-computer"></a>如何：枚举计算机上存在的时区

若要成功使用指定的时区，需要该时区的相关信息可供系统使用。 在 Windows XP 和 Windows Vista 操作系统在注册表中存储此信息。 但是，尽管世界上存在的时区总数非常大，但注册表包含的信息只是其中的一个子集。 此外，注册表本身是一个动态结构，其内容可能发生有意或无意的更改。 因此，应用程序无法保证系统上始终存在已定义且可用的特定时区。 对于使用时区信息应用程序的许多应用程序来说，第一步是确定所需时区在本地系统上是否可用，或者向用户提供可供选择的时区列表。 这要求应用程序枚举本地系统上定义的时区。

> [!NOTE]
> 如果应用程序依赖于本地系统可能没有定义某个特定时区的存在，应用程序可以确保其存在的序列化和反序列化时间区域相关信息。 时区然后可以添加到列表控件，以便应用程序用户可以选择它。 有关详细信息，请参阅[如何：将时区保存到嵌入的资源](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md)和[如何：从嵌入的资源还原时区](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md)。

### <a name="to-enumerate-the-time-zones-present-on-the-local-system"></a>枚举本地系统上存在的时区

1. 调用 <xref:System.TimeZoneInfo.GetSystemTimeZones%2A?displayProperty=nameWithType> 方法。 该方法返回一个泛型<xref:System.Collections.ObjectModel.ReadOnlyCollection%601>的集合<xref:System.TimeZoneInfo>对象。 集合中的项将按其<xref:System.TimeZoneInfo.DisplayName%2A>属性。 例如：

   [!code-csharp[System.TimeZone2.Concepts#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#1)]
   [!code-vb[System.TimeZone2.Concepts#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#1)]

2. 枚举各个<xref:System.TimeZoneInfo>通过使用集合中的对象`foreach`循环 （在 C# 中) 或`For Each`...`Next` 循环 （在 Visual Basic 中)，并对每个对象执行任何必要的处理。 例如，下面的代码枚举<xref:System.Collections.ObjectModel.ReadOnlyCollection%601>的集合<xref:System.TimeZoneInfo>对象步骤 1 中返回，并列出了在控制台上每个时区的显示名称。

   [!code-csharp[System.TimeZone2.Concepts#12](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#12)]
   [!code-vb[System.TimeZone2.Concepts#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#12)]

### <a name="to-present-the-user-with-a-list-of-time-zones-present-on-the-local-system"></a>若要为用户提供的本地系统上存在的时区列表

1. 调用 <xref:System.TimeZoneInfo.GetSystemTimeZones%2A?displayProperty=nameWithType> 方法。 该方法返回一个泛型<xref:System.Collections.ObjectModel.ReadOnlyCollection%601>的集合<xref:System.TimeZoneInfo>对象。

2. 将分配到的步骤 1 中返回的集合`DataSource`属性的 Windows 窗体或 ASP.NET 列表控件。

3. 检索<xref:System.TimeZoneInfo>用户选定的对象。

该示例说明了为 Windows 应用程序。

## <a name="example"></a>示例

该示例启动一个 Windows 应用程序，将显示一个列表框中的系统上定义的时区。 该示例然后显示一个对话框，其中包含的值<xref:System.TimeZoneInfo.DisplayName%2A>用户所选时区对象的属性。

[!code-csharp[System.TimeZone2.Concepts#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#2)]
[!code-vb[System.TimeZone2.Concepts#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#2)]

大多数 list 控件 (如<xref:System.Windows.Forms.ListBox?displayProperty=nameWithType>或<xref:System.Web.UI.WebControls.BulletedList?displayProperty=nameWithType>控件) 使你能够分配到的对象变量的集合及其`DataSource`属性，只要该集合实现<xref:System.Collections.IEnumerable>接口。 (泛型<xref:System.Collections.ObjectModel.ReadOnlyCollection%601>类就是如此。)若要在集合中显示的单个对象，该控件调用该对象的`ToString`方法以提取用于表示对象的字符串。 情况下<xref:System.TimeZoneInfo>对象，`ToString`方法将返回<xref:System.TimeZoneInfo>对象的显示名称 (的值及其<xref:System.TimeZoneInfo.DisplayName%2A>属性)。

> [!NOTE]
> 因为列表控件调用对象的`ToString`方法，可以分配一系列<xref:System.TimeZoneInfo>对象控制，让控件显示每个对象，有意义的名称，并检索<xref:System.TimeZoneInfo>用户选定的对象。 这消除了需要提取每个对象在集合中的字符串，将字符串分配给一个集合，其中又分配给控件的`DataSource`属性，检索用户，已选中，该字符串，并使用此字符串中提取对象其中描述了。 

## <a name="compiling-the-code"></a>编译代码

此示例需要：

* 包含对 System.Core.dll 的引用添加到项目。

* 将导入以下命名空间：

  <xref:System> （在 C# 代码中）

  <xref:System.Collections.ObjectModel>

## <a name="see-also"></a>请参阅

- [日期、时间和时区](../../../docs/standard/datetime/index.md)
- [如何：将时区保存到嵌入的资源](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md)
- [如何：从嵌入的资源还原时区](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md)
