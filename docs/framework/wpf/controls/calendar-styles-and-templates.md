---
title: Calendar 样式和模板
ms.date: 03/30/2017
helpviewer_keywords:
- styles [WPF], Calendar
- templates [WPF], Calendar
- states [WPF], Calendar
- parts [WPF], Calendar
- Calendar [WPF], styles and templates
- ControlTemplate [WPF], Calendar
ms.assetid: f4fcf046-7a8f-41b8-b5a8-534b64e0345c
ms.openlocfilehash: beba15f12b0ae2b819c641de9af8485767ad1a78
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57373408"
---
# <a name="calendar-styles-and-templates"></a>Calendar 样式和模板
本主题介绍的样式和模板的<xref:System.Windows.Controls.Calendar>控件。 可以修改默认<xref:System.Windows.Controls.ControlTemplate>为控件提供唯一外观。 有关详细信息，请参阅[通过创建 ControlTemplate 自定义现有控件的外观](customizing-the-appearance-of-an-existing-control.md)。  
  
## <a name="calendar-parts"></a>日历部件  
 下表列出了用于命名的部件<xref:System.Windows.Controls.Calendar>控件。  
  
|部件|类型|描述|  
|-|-|-|  
|PART_CalendarItem|<xref:System.Windows.Controls.Primitives.CalendarItem>|当前显示的月份或年份上的<xref:System.Windows.Controls.Calendar>。|  
|PART_Root|<xref:System.Windows.Controls.Panel>|面板，其中包含<xref:System.Windows.Controls.Primitives.CalendarItem>。|  
  
## <a name="calendar-states"></a>日历状态  
 下表列出了的可视状态<xref:System.Windows.Controls.Calendar>控件。  
  
|VisualState 名称|VisualStateGroup 名称|描述|  
|----------------------|---------------------------|-----------------|  
|有效|ValidationStates|该控件使用<xref:System.Windows.Controls.Validation>类和<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType>附加的属性是`false`。|  
|InvalidFocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType>附加的属性是`true`已在控件有焦点。|  
|InvalidUnfocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType>附加的属性是`true`具有该控件没有焦点。|  
  
## <a name="calendaritem-parts"></a>日历项目部分  
 下表列出了用于命名的部件<xref:System.Windows.Controls.Primitives.CalendarItem>控件。  
  
|部件|类型|描述|  
|-|-|-|  
|PART_Root|<xref:System.Windows.FrameworkElement>|控件的根。|  
|PART_PreviousButton|<xref:System.Windows.Controls.Button>|单击它时，显示日历的前一页按钮。|  
|PART_NextButton|<xref:System.Windows.Controls.Button>|该按钮将显示日历的下一页面时单击它。|  
|PART_HeaderButton|<xref:System.Windows.Controls.Button>|允许在月模式、 年模式和十年模式之间切换按钮。|  
|PART_MonthView|<xref:System.Windows.Controls.Grid>|承载在月模式下的内容。|  
|PART_YearView|<xref:System.Windows.Controls.Grid>|承载在年或十年中的模式下的内容。|  
|PART_DisabledVisual|<xref:System.Windows.FrameworkElement>|在覆盖区上为禁用状态的。|  
|DayTitleTemplate|<xref:System.Windows.DataTemplate>|<xref:System.Windows.DataTemplate>描述可视结构。|  
  
## <a name="calendaritem-states"></a>日历项目状态  
 下表列出了的可视状态<xref:System.Windows.Controls.Primitives.CalendarItem>控件。  
  
|VisualState 名称|VisualStateGroup 名称|描述|  
|-|-|-|  
|正常状态|CommonStates|默认状态。|  
|已禁用状态|CommonStates|日历的状态时<xref:System.Windows.UIElement.IsEnabled%2A>属性是`false`。|  
|有效|ValidationStates|该控件使用<xref:System.Windows.Controls.Validation>类和<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType>附加的属性是`false`。|  
|InvalidFocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType>附加的属性是`true`已在控件有焦点。|  
|InvalidUnfocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType>附加的属性是`true`具有该控件没有焦点。|  
|有效|ValidationStates|该控件使用<xref:System.Windows.Controls.Validation>类和<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType>附加的属性是`false`。|  
|InvalidFocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType>附加的属性是`true`已在控件有焦点。|  
|InvalidUnfocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType>附加的属性是`true`具有该控件没有焦点。|  
  
## <a name="calendardaybutton-parts"></a>CalendarDayButton 部件  
 <xref:System.Windows.Controls.Primitives.CalendarDayButton>控件没有任何命名的部件。  
  
## <a name="calendardaybutton-states"></a>CalendarDayButton 状态  
 下表列出了的可视状态<xref:System.Windows.Controls.Primitives.CalendarDayButton>控件。  
  
|VisualState 名称|VisualStateGroup 名称|描述|  
|-|-|-|  
|普通|CommonStates|默认状态。|  
|已禁用|CommonStates|<xref:System.Windows.Controls.Primitives.CalendarDayButton>被禁用。|  
|MouseOver|CommonStates|鼠标指针置于<xref:System.Windows.Controls.Primitives.CalendarDayButton>。|  
|已按下|CommonStates|<xref:System.Windows.Controls.Primitives.CalendarDayButton>按下。|  
|已选定|SelectionStates|按钮处于选中状态。|  
|未选定|SelectionStates|未选择该按钮。|  
|CalendarButtonFocused|CalendarButtonFocusStates|该按钮具有焦点。|  
|CalendarButtonUnfocused|CalendarButtonFocusStates|该按钮不具有焦点。|  
|已设定焦点|FocusStates|该按钮具有焦点。|  
|失去焦点|FocusStates|该按钮不具有焦点。|  
|活动的|ActiveStates|该按钮处于活动状态。|  
|非活动状态|ActiveStates|该按钮处于非活动状态。|  
|RegularDay|DayStates|该按钮不表示<xref:System.DateTime.Today%2A?displayProperty=nameWithType>。|  
|今天|DayStates|此按钮表示<xref:System.DateTime.Today%2A?displayProperty=nameWithType>。|  
|NormalDay|BlackoutDayStates|此按钮表示可以选择一天。|  
|BlackoutDay|BlackoutDayStates|此按钮表示不能选择一天。|  
|有效|ValidationStates|该控件使用<xref:System.Windows.Controls.Validation>类和<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType>附加的属性是`false`。|  
|InvalidFocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType>附加的属性是`true`已在控件有焦点。|  
|InvalidUnfocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType>附加的属性是`true`具有该控件没有焦点。|  
  
## <a name="calendarbutton-parts"></a>CalendarButton 部件  
 <xref:System.Windows.Controls.Primitives.CalendarButton>控件没有任何命名的部件。  
  
## <a name="calendarbutton-states"></a>CalendarButton 状态  
 下表列出了的可视状态<xref:System.Windows.Controls.Primitives.CalendarButton>控件。  
  
|VisualState 名称|VisualStateGroup 名称|描述|  
|-|-|-|  
|普通|CommonStates|默认状态。|  
|已禁用|CommonStates|<xref:System.Windows.Controls.Primitives.CalendarButton>被禁用。|  
|MouseOver|CommonStates|鼠标指针置于<xref:System.Windows.Controls.Primitives.CalendarButton>。|  
|已按下|CommonStates|<xref:System.Windows.Controls.Primitives.CalendarButton>按下。|  
|已选定|SelectionStates|按钮处于选中状态。|  
|未选定|SelectionStates|未选择该按钮。|  
|CalendarButtonFocused|CalendarButtonFocusStates|该按钮具有焦点。|  
|CalendarButtonUnfocused|CalendarButtonFocusStates|该按钮不具有焦点。|  
|已设定焦点|FocusStates|该按钮具有焦点。|  
|失去焦点|FocusStates|该按钮不具有焦点。|  
|活动的|ActiveStates|该按钮处于活动状态。|  
|非活动状态|ActiveStates|该按钮处于非活动状态。|  
|有效|ValidationStates|该控件使用<xref:System.Windows.Controls.Validation>类和<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType>附加的属性是`false`。|  
|InvalidFocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType>附加的属性是`true`已在控件有焦点。|  
|InvalidUnfocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType>附加的属性是`true`具有该控件没有焦点。|  
  
## <a name="calendar-controltemplate-example"></a>日历 ControlTemplate 示例  
 下面的示例演示如何定义<xref:System.Windows.Controls.ControlTemplate>为<xref:System.Windows.Controls.Calendar>控件和关联的类型。  
  
 [!code-xaml[ControlTemplateExamples#Calendar](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/calendar.xaml#calendar)]  
  
 上一示例使用了一个或多个以下资源。  
  
 [!code-xaml[ControlTemplateExamples#Resources](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/shared.xaml#resources)]  
  
 有关完整示例，请参阅[使用 ControlTemplates 设置样式示例](https://github.com/Microsoft/WPF-Samples/tree/master/Styles%20&%20Templates/IntroToStylingAndTemplating)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.FrameworkElement.Style%2A>
- <xref:System.Windows.Controls.ControlTemplate>
- [控件样式和模板](control-styles-and-templates.md)
- [控件自定义](control-customization.md)
- [样式设置和模板化](styling-and-templating.md)
- [通过创建 ControlTemplate 自定义现有控件的外观](customizing-the-appearance-of-an-existing-control.md)
