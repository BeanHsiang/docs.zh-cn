---
title: Windows 窗体添加配置元素
ms.date: 04/07/2017
helpviewer_keywords:
- Windows Forms Add configuration element
- configuring Windows Forms applications
ms.assetid: 3e3e04de-99d1-4658-b716-44cb669d9589
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: eca84aa3a3d7bffaac31cc36ed14e5d5bb5a37cc
ms.sourcegitcommit: 5d9f4b805787f890ca6e0dc7ea30a43018bc9cbb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2019
ms.locfileid: "57788474"
---
# <a name="windows-forms-add-configuration-element"></a>Windows 窗体添加配置元素

`<add>`元素将添加指定 Windows 窗体应用程序是否支持添加到 Windows 窗体应用程序在.NET Framework 4.7 或更高版本的功能的预定义的键。

## <a name="syntax"></a>语法

```xml
<System.Windows.Forms.ApplicationConfigurationSection>
  <add key="key-name" value="key-value" />
</System.Windows.Forms.ApplicationConfigurationSection>
```

## <a name="attributes-and-elements"></a>特性和元素

下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

| 特性 | 描述 |
| --------- | ----------- |
| `key`     | 必需的特性。 对应到特定的 Windows 窗体可自定义功能的预定义的名称。 |
| `value`   | 必需的特性。 要赋给 `key` 的值。 |

### <a name="key-attribute-names-and-associated-values"></a>`key` 属性名称和关联的值

| `key` 名称 | 值 | 描述 |
| ---------- | ------ | ----------- |
| "AnchorLayout.DisableSinglePassControlScaling" | "true"&#124;"false" | 指示是否在单个传递中缩放锚定的控件。 "true"，以禁用单个传递缩放;否则为 false。 请参阅中的"单传递缩放"一节[备注](#remarks)有关详细信息。 |
| "DpiAwareness" | "PerMonitorV2"&#124;"false" | 指示是否为高 dpi 应用程序。 将键设置为"PerMonitorV2"，以支持 Dpi 识别;否则，将其设置为"false"。 DPI 识别是一项选择加入的功能;若要充分利用 Windows 窗体的高 DPI 支持，应设置其值为"PerMonitorV2"。 请参阅[备注](#remarks)部分，了解详细信息。 |
| "CheckedListBox.DisableHighDpiImprovements" | "true"&#124;"false" | 指示是否<xref:System.Windows.Forms.CheckedListBox>控件利用的缩放和布局在.NET Framework 4.7 中引入的改进。 "true"即可选择退出 caling 和布局方面的改进;否则为"false"。 |
| "DataGridView.DisableHighDpiImprovements" | "true"&#124;"false" | 指示是否<xref:System.Windows.Forms.DataGridView>控制在.NET Framework 4.7 中引入的缩放和布局改进。 "true"即可选择退出 DPI 识别;"false"否则为。 |
| "DisableDpiChangedMessageHandling" | "true"&#124;"false" | "true"来选择不接收 DPI 缩放的更改，为与相关的消息"false"否则为。 请参阅[备注](#remarks)部分，了解详细信息。 |
| "EnableWindowsFormsHighDpiAutoResizing" | "true"&#124;"false" | 指示是否自动调整 Windows 窗体应用程序大小由于 DPI 缩放的更改。 "true"以启用自动调整大小;否则为 false。 |
| "Form.DisableSinglePassControlScaling" | "true"&#124;"false" | 指示是否<xref:System.Windows.Forms.Form>缩放单个传递中。 "true"，以禁用单步缩放;否则为 false。 请参阅中的"单传递缩放"一节[备注](#remarks)有关详细信息。 |
| "MonthCalendar.DisableSinglePassControlScaling" | "true"&#124;"false" | 指示是否<xref:System.Windows.Forms.MonthCalendar>单个传递中缩放控件。 "true"，以禁用单步缩放;否则为 false。 请参阅中的"单传递缩放"一节[备注](#remarks)有关详细信息。 |
| "Toolstrip.DisableHighDpiImprovements" | "true"&#124;"false" | 指示是否<xref:System.Windows.Forms.ToolStrip>控件利用的缩放和布局在.NET Framework 4.7 中引入的改进。 "true"即可选择退出 DPI 识别;"false"否则为。 |

### <a name="child-elements"></a>子元素

无。

### <a name="parent-elements"></a>父元素

| 元素 | 描述 |
| ------- | ----------- |
| [`<System.Windows.Forms.ApplicationConfigurationSection>`](../../../../../docs/framework/configure-apps/file-schema/winforms/index.md) | 配置对新 Windows 窗体应用程序功能的支持。 |

## <a name="remarks"></a>备注

从 .NET Framework 4.7 开始，`<System.Windows.Forms.ApplicationConfigurationSection>` 元素允许配置 Windows 窗体应用程序，以利用最新版本的 .NET Framework 中添加的功能。

`<System.Windows.Forms.ApplicationConfigurationSection>`元素允许您添加一个或多个子级`<add>`元素，其中每个定义特定的配置设置。

Windows 窗体高 DPI 支持的概述，请参阅[在 Windows 窗体中的高 DPI 支持](../../../../../docs/framework/winforms/high-dpi-support-in-windows-forms.md)。

### <a name="dpiawareness"></a>DpiAwareness

从.NET Framework 4.7 开始使用 Windows 10 创意者版本和.NET Framework 版本的 Windows 版本下运行的 Windows 窗体应用程序可以配置为充分利用.NET Framework 中引入的高 DPI 改进4.7。 这些问题包括：

- 对 Windows 窗体应用程序已启动后在用户更改 DPI 或缩放系数的动态 DPI 方案的支持。

- 改进的缩放和多个 Windows 窗体的布局控件，如<xref:System.Windows.Forms.MonthCalendar>控件和<xref:System.Windows.Forms.CheckedListBox>控件。

高 DPI 识别是一项选择加入的功能;默认情况下的值`DpiAwareness`是`false`。 你可以选择加入 Windows 窗体支持的 DPI 识别到此密钥的值设置`PerMonitorV2`应用程序配置文件中。 如果启用 DPI 识别，则还会启用所有单独的 DPI 功能。 这些问题包括：

- DPI 更改受控制的消息`DisableDpiChangedMessageHandling`密钥。

- 动态 DPI 支持，由控制`EnableWindowsFormsHighDpiAutoResizing`密钥。

- 单次传递控制缩放，这受`Form.DisableSinglePassControlScaling`为各个<xref:System.Windows.Forms.Form>控件，通过`AnchorLayout.DisableSinglePassControlScaling`锚定控件，并通过密钥`MonthCalendar.DisableSinglePassControlScaling`密钥对<xref:System.Windows.Forms.MonthCalendar>控件

- 高 DPI 缩放和布局方面的改进，通过控制`CheckListBox.DisableHighDpiImprovements`密钥对<xref:System.Windows.Forms.CheckedListBox>控件，通过`DataGridView.DisableHighDpiImprovements`密钥对<xref:System.Windows.Forms.DataGridView>控件，并通过`Toolstrip.DisableHighDpiImprovements`密钥对<xref:System.Windows.Forms.ToolStrip>控件。

通过设置提供选择中设置一个默认`DpiAwareness`到`PerMonitorV2`通常足以满足新的 Windows 窗体应用程序。 但是，你可以然后选择退出各个高 DPI 改进通过将相应的密钥添加到应用程序配置文件。 例如，若要利用动态 DPI 支持除外的所有新 DPI 功能，要到应用程序配置文件添加以下：

```xml
<System.Windows.Forms.ApplicationConfigurationSection>
   <add key="DpiAwareness" value="PerMonitorV2" />
   <!-- Disable dynamic DPI support -->
   <add key="EnableWindowsFormsHighDpiAutoResizing" value="false" />
</System.Windows.Forms.ApplicationConfigurationSection>
```

通常情况下，您选择禁用特定功能因为您已选择了以编程方式对其进行处理。

可利用在 Windows 窗体应用程序中的高 DPI 支持的详细信息，请参阅[在 Windows 窗体中的高 DPI 支持](../../../../../docs/framework/winforms/high-dpi-support-in-windows-forms.md)。

### <a name="disabledpichangedmessagehandling"></a>DisableDpiChangedMessageHandling

从.NET Framework 4.7 开始，Windows 窗体控件引发 DPI 缩放的更改相关的事件的数。 其中包括<xref:System.Windows.Forms.Control.DpiChangedAfterParent>， <xref:System.Windows.Forms.Control.DpiChangedBeforeParent>，和<xref:System.Windows.Forms.Form.DpiChanged>事件。 值`DisableDpiChangedMessageHandling`密钥确定是否在 Windows 窗体应用程序中引发这些事件。

### <a name="single-pass-scaling"></a>单次传递缩放

单个或多通路缩放影响感知的响应性的用户界面和用户界面元素的可视外观，因为它们缩放。 从.NET Framework 4.7 开始，使用单个传递缩放 Windows 窗体。 在以前版本的.NET Framework 中，通过多个通过，这导致一些控件，以扩展超过需要执行缩放。 如果您的应用程序依赖旧行为应仅禁用单次传递缩放。

## <a name="see-also"></a>请参阅

- [Windows 窗体配置节](../../../../../docs/framework/configure-apps/file-schema/winforms/index.md)
- [Windows 窗体中的高 DPI 支持](../../../../../docs/framework/winforms/high-dpi-support-in-windows-forms.md)
