---
title: .NET Framework 中辅助功能的新增功能
ms.custom: updateeachrelease
ms.date: 04/10/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- what's new [.NET Framework]
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2bdb1bf5d7e32c2e05eb779eed16c311cbd3eae7
ms.sourcegitcommit: 79066169e93d9d65203028b21983574ad9dcf6b4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57212503"
---
# <a name="whats-new-in-accessibility-in-the-net-framework"></a>.NET Framework 中辅助功能的新增功能

.NET Framework 旨在让用户更轻松地使用应用程序。 辅助功能使应用程序能够为辅助技术用户提供最佳体验。 从 .NET Framework 4.7.1 开始，.NET Framework 包括大量辅助功能改进，使开发人员能够创建易于访问的应用程序。

## <a name="accessibility-switches"></a>辅助功能开关

如果应用面向 .NET Framework 4.7 或更低版本，但是在 .NET Framework 4.7.1 或更高版本上运行，可以将应用配置为选择使用辅助功能。 如果应用面向 .NET Framework 4.7.1 或更高版本，还可以将应用配置为使用旧版功能（且不使用辅助功能）。 包括辅助功能的每个 .NET Framework 版本都有一个特定于版本的辅助开关，请将它添加到应用程序配置文件 [`<runtime>`](~/docs/framework/configure-apps/file-schema/runtime/index.md) 部分中的 [`<AppContextSwitchOverrides>`](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 元素。 以下是受支持的开关：

|Version|开关|
|---|---|
|.NET Framework 4.7.1|"Switch.UseLegacyAccessibilityFeatures"|
|.NET Framework 4.7.2|"Switch.UseLegacyAccessibilityFeatures.2"|

### <a name="taking-advantage-of-accessibility-enhancements"></a>利用辅助功能改进

对于面向 .NET Framework 4.7.1 或更高版本的应用程序，新的辅助功能默认情况下处于启用状态。 此外，对于面向 .NET Framework 早期版本，但在 .NET Framework 4.7.1 或更高版本上运行的应用程序，可通过将开关添加到应用程序配置文件 [`<runtime>`](~/docs/framework/configure-apps/file-schema/runtime/index.md) 部分中的 [`<AppContextSwitchOverrides>`](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 元素并将其值设为 `false` 来选择弃用旧辅助功能行为（因而利用辅助功能改进）。 以下代码演示如何选择使用 .NET Framework 4.7.1 中引入的辅助功能改进：

```xml
<runtime>
    <!-- AppContextSwitchOverrides value attribute is in the form of 'key1=true|false;key2=true|false  -->
    <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false" />
</runtime>
```

如果选择使用更高的 .NET Framework 版本中的辅助功能，还必须显式选择使用更低 .NET Framework 版本的功能。 将应用配置为利用 .NET Framework 4.7.1 和 4.7.2 中的辅助功能改进需要以下 [`<AppContextSwitchOverrides>`](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 元素：

```xml
<runtime>
    <!-- AppContextSwitchOverrides value attribute is in the form of 'key1=true|false;key2=true|false  -->
    <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false" />
</runtime>
```

### <a name="restoring-legacy-behavior"></a>还原旧行为

对于面向 .NET Framework 4.7.1 或更高版本的应用程序，可通过将开关添加到应用程序配置文件 [`<runtime>`](~/docs/framework/configure-apps/file-schema/runtime/index.md) 部分中的 [`<AppContextSwitchOverrides>`](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 元素并将其值设为 `true` 来禁用辅助功能。 例如，以下配置选择弃用 .NET Framework 4.7.2 中引入的辅助功能：

```xml
<runtime>
    <!-- AppContextSwitchOverrides value attribute is in the form of 'key1=true|false;key2=true|false  -->
    <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures.2=true" />
</runtime>
```

## <a name="whats-new-in-accessibility-in-the-net-framework-472"></a>.NET Framework 4.7.2 中辅助功能的新增功能

.NET Framework 4.7.2 在以下几个领域新增了辅助功能：

- [Windows 窗体](#winforms472)

- [Windows Presentation Foundation (WPF)](#wpf472)

<a name="winforms472"></a>

### <a name="windows-forms"></a>Windows 窗体

**高对比度主题中的 OS 定义的颜色**

自 .NET Framework 4.7.2 起，Windows 窗体使用高对比度主题中的操作系统定义的颜色。 这会影响以下控件：

- <xref:System.Windows.Forms.ToolStripDropDownButton> 控件的下拉箭头。

- <xref:System.Windows.Forms.ButtonBase.FlatStyle> 设为 <xref:System.Windows.Forms.FlatStyle.Flat?displayProperty=nameWithType> 或 <xref:System.Windows.Forms.FlatStyle.Popup?displayProperty=nameWithType> 的 <xref:System.Windows.Forms.Button>、<xref:System.Windows.Forms.RadioButton> 和 <xref:System.Windows.Forms.CheckBox> 控件。 以前，所选文本和背景颜色对比度低，难以阅读。

- <xref:System.Windows.Forms.Control.Enabled> 属性设为 `false` 的 <xref:System.Windows.Forms.GroupBox> 中所包含的控件。

- 在高对比度模式下，<xref:System.Windows.Forms.ToolStripButton>、<xref:System.Windows.Forms.ToolStripComboBox> 和 <xref:System.Windows.Forms.ToolStripDropDownButton> 控件的亮度对比度提高。

- <xref:System.Windows.Forms.DataGridViewLinkCell> 的 <xref:System.Windows.Forms.DataGridViewLinkCell.LinkColor> 属性。

**讲述人改进**

自 .NET Framework 4.7.2 起，讲述人支持在以下几个方面改进：

- 它在公布 <xref:System.Windows.Forms.ToolStripMenuItem> 的文本时会公布 <xref:System.Windows.Forms.ToolStripMenuItem.ShortcutKeys?displayProperty=nameWithType> 属性的值。

- 当 <xref:System.Windows.Forms.ToolStripMenuItem> 的 <xref:System.Windows.Forms.Control.Enabled> 属性设置为 `false` 时，它会有所指示。

- 当 <xref:System.Windows.Forms.ListView.CheckBoxes?displayProperty=nameWithType> 属性设置为 `true` 时，它会针对复选框的状态给出反馈。

- 讲述人扫描模式焦点顺序与 ClickOnce 下载对话框窗口中控件的视觉顺序一致。

**DataGridView 改进**

自 .NET Framework 4.7.2 起，<xref:System.Windows.Forms.DataGridView> 控件引入了以下辅助功能改进：

- 可以使用键盘对行进行排序。 用户可使用 F3 按当前列排序。

- 若 <xref:System.Windows.Forms.DataGridView.SelectionMode?displayProperty=nameWithType> 设置为 <xref:System.Windows.Forms.DataGridViewSelectionMode.FullRowSelect?displayProperty=nameWithType>，当用户按 Tab 键遍历当前行中的单元格时，列标题将更改颜色来指示当前列。

- <xref:System.Windows.Forms.DataGridViewLinkCell.DataGridViewLinkCellAccessibleObject?displayProperty=nameWithType> 的 <xref:System.Windows.Forms.AccessibleObject.Parent?displayProperty=nameWithType> 属性返回正确的父控件。

**改进了视觉提示**

- 具有空 <xref:System.Windows.Forms.ButtonBase.Text> 属性的 <xref:System.Windows.Forms.RadioButton> 和 <xref:System.Windows.Forms.CheckBox> 控件在接收到焦点时会显示焦点指示器。

**改进了属性网格支持**

- 现在，仅在 PropertyGrid 元素启用时，<xref:System.Windows.Forms.PropertyGrid> 控件子元素才会为 <xref:System.Windows.Automation.ValuePattern.IsReadOnlyProperty> 属性返回 `true`。

- 仅在用户可更改 PropertyGrid 元素时，<xref:System.Windows.Forms.PropertyGrid> 控件子元素才会为 <xref:System.Windows.Automation.AutomationElement.IsEnabledProperty> 属性返回 `false`。

**改进了的键盘导航**

- <xref:System.Windows.Forms.ToolStripButton> 控件允许在焦点包含在 <xref:System.Windows.Forms.ToolStripPanel>（其 <xref:System.Windows.Forms.ToolStripPanel.TabStop> 属性设置为 `true`）中时进行聚焦

<a name="wpf472"></a>

### <a name="windows-presentation-foundation-wpf"></a>Windows Presentation Foundation (WPF)

**对复选框和单选按钮控件的更改**

在 .NET Framework 4.7.1 和更低版本中，WPF <xref:System.Windows.Controls.CheckBox?displayProperty=nameWIthType> 和 <xref:System.Windows.Controls.RadioButton?displayProperty=nameWIthType> 控件不一致且在经典和高对比度主题中具有不正确的焦点视觉对象。  控件没有内容集时会出现这些问题。  这会使得主题间的转换变得混乱且难以看到焦点视觉对象。

现在，在 .NET Framework 4.7.2 中，主题间的这些视觉对象更加一致，并且在经典和高对比度主题中更轻松可见。

**在 WPF 应用程序中托管的 WinForms 控件**

对于 .NET Framework 4.7.1 和更低版本中的 WPF 应用程序托管的 WinForms 控件，如果该层中的第一个或最后一个控件是 WPF <xref:System.Windows.Forms.Integration.ElementHost> 控件，那么用户不能按 Tab 退出 WinForms 层。 现在，在 .NET Framework 4.7.2 中，用户能够按 Tab 退出 WinForms 层。

但是，依赖于永不转义 WinForms 层的焦点的自动化应用程序不再会按预期工作。

## <a name="whats-new-in-accessibility-in-the-net-framework-471"></a>.NET Framework 4.7.1 中辅助功能的新增功能

.NET Framework 4.7.1 在以下几个领域新增了辅助功能：

- [Windows Presentation Foundation (WPF)](#wpf471)

- [Windows 窗体](#winforms471)

- [ASP.NET Web 控件](#aspnet471)

- [.NET SDK 工具](#tools471)

- [Windows Workflow Foundation (WF) 工作流设计器](#wf471)

<a name="wpf471"></a>

### <a name="windows-presentation-foundation-wpf"></a>Windows Presentation Foundation (WPF)

**屏幕阅读器改进**

如果启用了辅助功能改进，.NET Framework 4.7.1 包括以下可影响屏幕读阅读的增强功能：

- 在 .NET Framework 4.7 及更低版本中，<xref:System.Windows.Controls.Expander> 控件由屏幕阅读器宣称为按钮。 从 .NET Framework 4.7.1 开始，它们被正确地称为可展开/可折叠组。

- 在 .NET Framework 4.7 及更低版本中，<xref:System.Windows.Controls.DataGridCell> 控件由屏幕阅读器宣称为“自定义”。 从 .NET Framework 4.7.1 开始，它们被正确地称为数据网格单元格（已本地化）。

- 从 .NET Framework 4.7.1 开始，屏幕阅读器读出可编辑 <xref:System.Windows.Controls.ComboBox> 的名称。

- 在 .NET Framework 4.7 及更低版本中，<xref:System.Windows.Controls.PasswordBox> 控件被宣称为“视图中没有任何项”或有其他错误行为。 此问题已在 .NET Framework 4.7.1 及更高版本中解决。

**UIAutomation LiveRegion 支持**

屏幕阅读器（如讲述人）可帮助用户阅读应用程序的 UI 内容，通常通过具有焦点的 UI 内容的文本到语音转换输出实现。 但是，如果 UI 元素更改，并且不具有焦点，则用户可能不会收到通知，并且可能会错过重要信息。 活动区域旨在解决此问题。 开发人员可使用它们来通知屏幕阅读器或任何其他 UIAutomation 客户端 UI 元素有重要更改。 然后，屏幕阅读器可确定向用户通知此更改的方式和时间。

为了支持活动区域，向 WPF 添加了以下 API：

- <xref:System.Windows.Automation.AutomationElementIdentifiers.LiveSettingProperty?displayProperty=nameWithType> 和 <xref:System.Windows.Automation.AutomationElementIdentifiers.LiveRegionChangedEvent?displayProperty=nameWithType> 字段，用于标识 LiveSetting 属性和 LiveRegionChanged 事件。 可通过使用 XAML 来进行设置。

- AutomationProperties.LiveSetting 附加属性，用于向屏幕阅读器通知 UI 更改对用户的重要性。

- <xref:System.Windows.Automation.AutomationProperties.LiveSettingProperty?displayProperty=nameWithType> 属性，用于标识 AutomationProperties.LiveSetting 附加属性。

- <xref:System.Windows.Automation.Peers.AutomationPeer.GetLiveSettingCore%2A?displayProperty=nameWithType> 方法，可替代该方法以提供 LiveSetting 值。

- <xref:System.Windows.Automation.AutomationProperties.GetLiveSetting%2A?displayProperty=nameWithType> 和 <xref:System.Windows.Automation.AutomationProperties.SetLiveSetting%2A?displayProperty=nameWithType> 方法，用于获取和设置 LiveSetting 值。

- <xref:System.Windows.Automation.AutomationLiveSetting?displayProperty=nameWithType> 枚举，用于定义以下可能的 LiveSetting 值：

   - <xref:System.Windows.Automation.AutomationLiveSetting.Off?displayProperty=nameWithType>。 如果活动区域的内容已更改，则该元素不会发送通知。
   - <xref:System.Windows.Automation.AutomationLiveSetting.Polite?displayProperty=nameWithType>。 如果活动区域的内容已更改，则该元素将发送非中断通知。

   - <xref:System.Windows.Automation.AutomationLiveSetting.Assertive?displayProperty=nameWithType>。 如果活动区域的内容已更改，则该元素将发送中断通知。

可通过对相关元素设置 AutomationProperties.LiveSetting 属性来创建 LiveRegion，如以下示例所示：

```xaml
<TextBlock Name="myTextBlock" AutomationProperties.LiveSetting="Assertive">announcement</TextBlock>
```

活动区域中的数据发生更改，并且需要通知屏幕阅读器时，可显式引发事件，如以下示例所示。

```csharp
var peer = FrameworkElementAutomationPeer.FromElement(myTextBlock);

peer.RaiseAutomationEvent(AutomationEvents.LiveRegionChanged);
```
```vb
Dim peer = FrameworkElementAutomationPeer.FromElement(myTextBlock)
peer.RaiseAutomationEvent(AutomationEvents.LiveRegionChanged)

```

**高对比度**

从 .NET Framework 4.7.1 开始，对多种 WPF 控件进行了高对比度改进。 可在设置 <xref:System.Windows.SystemParameters.HighContrast%2A> 主题后看到这些改进。 这些方法包括：

- <xref:System.Windows.Controls.Expander> 控件

    <xref:System.Windows.Controls.Expander> 控件的焦点视觉对象现在可见。 <xref:System.Windows.Controls.ComboBox>、<xref:System.Windows.Controls.ListBox> 和 <xref:System.Windows.Controls.RadioButton> 控件的键盘视觉对象也可见。 例如:

    在此之前: 

    ![辅助功能改进前具有焦点的 Expander 控件](media/expander-before.png)

    之后： 

    ![辅助功能改进后具有焦点的 Expander 控件](media/expander-after.png)

- <xref:System.Windows.Controls.CheckBox> 和 <xref:System.Windows.Controls.RadioButton> 控件

    在高对比度主题下选中时，<xref:System.Windows.Controls.CheckBox> 和 <xref:System.Windows.Controls.RadioButton> 控件中的文本更易于查看。 例如:

    在此之前: 

    ![辅助功能改进前具有焦点的高对比度单选按钮](media/radio-button-before.png)

    之后： 

    ![辅助功能改进后具有焦点的高对比度单选按钮](media/radio-button-after.png)

- <xref:System.Windows.Controls.ComboBox> 控件

    从 .NET Framework 4.7.1 开始，已禁用的 <xref:System.Windows.Controls.ComboBox> 控件的边框与禁用的文本颜色相同。 例如:

    在此之前: 

     ![辅助功能改进前禁用的 ComboBox 边框和文本](media/combo-disabled-before.png)

    之后：   

     ![辅助功能改进后禁用的 ComboBox 边框和文本](media/combo-disabled-after.png)

    此外，已禁用的按钮和具有焦点的按钮使用正确的主题颜色。

    在此之前:

    ![辅助功能改进前的按钮主题颜色](media/button-themes-before.png) 

    之后： 

    ![辅助功能改进后的按钮主题颜色](media/button-themes-after.png) 

    最后，在 .NET Framework 4.7 及更低版本中，将 <xref:System.Windows.Controls.ComboBox> 控件的样式设置为 `Toolbar.ComboBoxStyleKey` 会导致下拉箭头不可见。 此问题已在 .NET Framework 4.7.1 及更高版本中解决。 例如:

    在此之前: 

    ![辅助功能改进前的 Toolbar.ComboBoxStyleKey](media/comboboxstylekey-before.png) 

    之后： 

    ![辅助功能改进后的 Toolbar.ComboBoxStyleKey](media/comboboxstylekey-after.png) 

- <xref:System.Windows.Controls.DataGrid> 控件

    从 .NET Framework 4.7.1 开始，<xref:System.Windows.Controls.DataGrid> 控件中的排序指示符箭头现在使用正确的主题颜色。 例如:

    在此之前: 

    ![辅助功能改进前的排序指示符箭头](media/sort-indicator-before.png) 

    之后：   

    ![辅助功能改进后的排序指示符箭头](media/sort-indicator-after.png) 

    此外，在 .NET Framework 4.7 及更低版本中，在高对比度模式下，默认链接样式在鼠标悬停在其上时更改为不正确的颜色。 此问题已在 .NET Framework 4.7.1 及更高版本中解决。 同样，从 .NET Framework 4.7.1 开始，<xref:System.Windows.Controls.DataGrid> 复选框列对键盘焦点反馈使用预期的颜色。

    在此之前: 

    ![辅助功能改进前的 DataGrid 默认链接样式](media/default-link-style-before.png) 

    之后：    

    ![辅助功能改进后的 DataGrid 默认链接样式](media/default-link-style-after.png) 

有关 .NET Framework 4.7.1 中 WPF 辅助功能改进的详细信息，请参阅 [WPF 辅助功能改进](../migration-guide/retargeting/4.7-4.7.1.md#accessibility-improvements-in-wpf)。

<a name="winforms471"></a>

### <a name="windows-forms-accessibility-improvements"></a>Windows 窗体辅助功能改进

在 .NET Framework 4.7.1 中，Windows 窗体 (WinForms) 包括以下几个方面的辅助功能改进。

**改进了高对比度模式下的显示**

从 .NET Framework 4.7.1 开始，多种 WinForms 控件改进了高对比度模式下在操作系统中的呈现方式。 Windows 10 更改了一些高对比度系统颜色的值，而 Windows 窗体基于 Windows 10 Win32 框架。 为获得最佳体验，请运行最新版本的 Windows，并通过在测试应用程序中添加 app.manifest 文件选择使用最新的 OS 更改，同时取消注释 Windows 10 支持的 OS 行，最终结果如下所示：

```xml
<!-- Windows 10 -->
<supportedOS Id=”{8e0f7a12-bfb3-4fe8-b9a5-48fd50a15a9a}” />
```

高对比度更改的一些示例包括：

- <xref:System.Windows.Forms.MenuStrip> 项中的复选标记更易于查看。

- 选中后，禁用的 <xref:System.Windows.Forms.MenuStrip> 项更易于查看。

- 所选 <xref:System.Windows.Forms.Button> 控件中的文本与选中颜色形成鲜明对比。

- 禁用的文本更易于阅读。 例如:

    在此之前:

    ![辅助功能改进前禁用的文本](media/wf-disabled-before.png) 

    之后：

    ![辅助功能改进后禁用的文本](media/wf-disabled-after.png) 

- “线程异常”对话框中的高对比度改进。

**改进了讲述人支持**

.NET Framework 4.7.1 中的 Windows 窗体对讲述人进行了以下辅助功改进：

- 讲述人以及其他 UI 自动化工具可访问 <xref:System.Windows.Forms.MonthCalendar> 控件。

- 当某个项的选中状态更改时，<xref:System.Windows.Forms.CheckedListBox> 控件会通知讲述人，因此用户可获知更改了列表项的值。

- <xref:System.Windows.Forms.DataGridViewCell> 控件向讲述人报告正确的只读状态。

- 讲述人现在可以阅读已禁用的 <xref:System.Windows.Forms.ToolStripMenuItem> 文本，而以前它会跳过禁用的菜单项。

**增强了对 UIAutomation 辅助功能模式的支持**

从 .NET Framework 4.7.1 开始，辅助功能技术工具的开发人员可以利用常见的 API 辅助功能模式和多个 WinForms 控件的属性。 这些辅助功能改进包括：

- <xref:System.Windows.Forms.ComboBox> 和 <xref:System.Windows.Forms.ToolStripSplitButton> 现在支持[展开/折叠模式](../ui-automation/implementing-the-ui-automation-expandcollapse-control-pattern.md)。

- <xref:System.Windows.Forms.DataGridViewCheckBoxCell> 现在支持[切换模式](../ui-automation/implementing-the-ui-automation-toggle-control-pattern.md)。

- <xref:System.Windows.Forms.ToolStripItem> 控件支持 <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.Name> 属性和[展开/折叠模式](../ui-automation/implementing-the-ui-automation-expandcollapse-control-pattern.md)。

- <xref:System.Windows.Forms.NumericUpDown> 和 <xref:System.Windows.Forms.DomainUpDown> 控件支持 <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.Name> 属性。

**改进了属性浏览器体验**

从 .NET Framework 4.7.1 开始，Windows 窗体包括以下改进：

- 更好地通过各种下拉选择窗口使用键盘导航。
- 减少不必要的制表位。
- 更好地报告控件类型。
- 改进了讲述人行为。

<a name="aspnet471"></a>

### <a name="aspnet-web-controls"></a>ASP.NET Web 控件

自 .NET Framework 4.7.1 和 Visual Studio 2017 15.3 起，ASP.NET 改进了 ASP.NET Web 控件与 Visual Studio 中的辅助功能技术配合使用的方式。 包括以下更改：

- 在以下控件中实现缺失 UI 的辅助功能模式：例如“详细信息视图”向导中的“添加字段”对话框或“ListView”向导的“配置 ListView”对话框。

- 改善在高对比度模式下（如“数据页导航字段编辑器”）的显示。

- 改善以下控件的键盘导航体验：例如 DataPager 控件的“编辑页导航字段”向导中的“字段”对话框、“配置 ObjectContext”对话框或“配置数据源”向导的“配置数据选择”对话框。

<a name="tools471"></a>

### <a name="net-sdk-tools"></a>.NET SDK 工具

[配置编辑器工具 (SvcConfigEditor.exe)](../wcf/configuration-editor-tool-svcconfigeditor-exe.md) 和[服务跟踪查看器工具 (SvcTraceViewer.exe)](../wcf/service-trace-viewer-tool-svctraceviewer-exe.md) 通过修复各种辅助功能问题得到改进。 其中大多数都是一些小问题，如未定义名称或未正确实现某些 UI 自动化模式。 虽然许多用户不会意识到这些小问题的重要性，但使用屏幕阅读器等辅助技术的客户会发现这些 SDK 工具更易于访问。

这些改进更改了某些旧行为，例如键盘焦点顺序。

<a name="wf471"></a>

### <a name="windows-workflow-foundation-wf-workflow-designer"></a>Windows Workflow Foundation (WF) 工作流设计器

工作流设计器中的辅助功能更改包括：

- 某些控件中 Tab 键顺序更改为从左到右以及从上到下：

  - 设置 <xref:System.ServiceModel.Activities.InitializeCorrelation> 活动相关数据的初始化相关窗口。

  - <xref:System.ServiceModel.Activities.Receive>、<xref:System.ServiceModel.Activities.Send>、<xref:System.ServiceModel.Activities.SendReply> 和 <xref:System.ServiceModel.Activities.ReceiveReply> 活动的内容定义窗口。

- 通过键盘可以使用更多功能：

  - 编辑活动的属性时，属性组在第一次聚焦时可以通过键盘折叠。

  - 警告图标可以通过键盘访问。

  - “属性”窗口的“更多属性”按钮可以通过键盘访问。

  - 键盘用户可以访问工作流设计器“参数”和“变量”窗格的标题项。

- 提升了聚焦项的可见性，例如当：

  - 将行添加到工作流设计器和活动设计器使用的数据网格。

  - 在 <xref:System.ServiceModel.Activities.ReceiveReply> 和 <xref:System.ServiceModel.Activities.SendReply> 活动中按 Tab 键切换字段。

  - 设置变量或自变量的默认值

- 屏幕读取器现在可以正确识别：

  - 工作流设计器中设置的断点。

  - <xref:System.Activities.Statements.FlowSwitch%601>、<xref:System.Activities.Statements.FlowDecision> 和 <xref:System.ServiceModel.Activities.CorrelationScope> 活动。
  - <xref:System.ServiceModel.Activities.Receive> 活动的内容。

  - <xref:System.Activities.Statements.InvokeMethod> 活动的目标类型。

  - <xref:System.Activities.Statements.TryCatch> 活动中的“异常”组合框和“最终”部分。

  - 消息传递活动（<xref:System.ServiceModel.Activities.Receive>、<xref:System.ServiceModel.Activities.Send>、<xref:System.ServiceModel.Activities.SendReply> 和 <xref:System.ServiceModel.Activities.ReceiveReply>）中的“消息类型”组合框、“添加相关初始化表达式”窗口中的拆分器、“内容定义”窗口和“CorrelatesOn 定义”窗口。

  - 状态机转换和转换目标。

  - <xref:System.Activities.Statements.FlowDecision> 活动上的注释和连接器。

  - 活动的上下文（右键单击）菜单。

  - 属性值编辑器、“清除搜索”按钮、“按类别”和“按字母顺序”排序按钮以及属性网格中的“表达式编辑器”对话框。

  - 工作流设计器中的缩放百分比。

  - <xref:System.Activities.Statements.Parallel> 和 <xref:System.Activities.Statements.Pick> 活动中的分隔符。

  - <xref:System.Activities.Statements.InvokeDelegate> 活动。

  - 字典活动（`Microsoft.Activities.AddToDictionary<TKey,TValue>`、`Microsoft.Activities.RemoveFromDictionary<TKey,TValue>` 等）的“选择类型”窗口。

  - “浏览和选择 .NET 类型”窗口。

  - 工作流设计器中的痕迹导航。

- 选择高对比度主题的用户将看到工作流设计器及其控件可见性的许多改进，例如元素间更好的对比度和焦点元素更明显的选择框。

## <a name="see-also"></a>请参阅

- [.NET Framework 的新增功能](whats-new.md)
