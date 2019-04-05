---
title: DatePicker 样式和模板
ms.date: 03/30/2017
helpviewer_keywords:
- ControlTemplate [WPF], DatePicker
- DatePicker [WPF], styles and templates
- templates [WPF], DatePicker
- parts [WPF], DatePicker
- styles [WPF], DatePicker
- states [WPF], DatePicker
ms.assetid: c430a657-692f-44bd-a549-2341f92d6115
ms.openlocfilehash: 685eb9478f1ff2da9047546648320a94305fff57
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57365277"
---
# <a name="datepicker-styles-and-templates"></a>DatePicker 样式和模板
本主题介绍的样式和模板的<xref:System.Windows.Controls.DatePicker>控件。 可以修改默认<xref:System.Windows.Controls.ControlTemplate>为控件提供唯一外观。 有关详细信息，请参阅[通过创建 ControlTemplate 自定义现有控件的外观](customizing-the-appearance-of-an-existing-control.md)。  
  
## <a name="datepicker-parts"></a>DatePicker 部件  
 下表列出了用于命名的部件<xref:System.Windows.Controls.DatePicker>控件。  
  
|部件|类型|描述|  
|-|-|-|  
|PART_Root|<xref:System.Windows.Controls.Grid>|控件的根。|  
|PART_Button|<xref:System.Windows.Controls.Button>|打开和关闭按钮<xref:System.Windows.Controls.Calendar>。|  
|PART_TextBox|<xref:System.Windows.Controls.Primitives.DatePickerTextBox>|使您能够输入日期的文本框。|  
|PART_Popup|<xref:System.Windows.Controls.Primitives.Popup>|为 popup<xref:System.Windows.Controls.DatePicker>控件。|  
  
## <a name="datepicker-states"></a>DatePicker 状态  
 下表列出了的可视状态<xref:System.Windows.Controls.DatePicker>控件。  
  
|VisualState 名称|VisualStateGroup 名称|描述|  
|-|-|-|  
|普通|CommonStates|默认状态。|  
|已禁用|CommonStates|<xref:System.Windows.Controls.DatePicker>被禁用。|  
|有效|ValidationStates|该控件使用<xref:System.Windows.Controls.Validation>类和<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType>附加的属性是`false`。|  
|InvalidFocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType>附加的属性是`true`已在控件有焦点。|  
|InvalidUnfocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType>附加的属性是`true`具有该控件没有焦点。|  
  
## <a name="datepickertextbox-parts"></a>DatePickerTextBox 部件  
 下表列出了用于命名的部件<xref:System.Windows.Controls.Primitives.DatePickerTextBox>控件。  
  
|部件|类型|描述|  
|-|-|-|  
|PART_Watermark|<xref:System.Windows.Controls.ContentControl>|包含中的初始文本的元素<xref:System.Windows.Controls.DatePicker>。|  
|PART_ContentElement|<xref:System.Windows.FrameworkElement>|可以包含一个可见元素<xref:System.Windows.FrameworkElement>。 文本<xref:System.Windows.Controls.TextBox>显示在此元素。|  
  
## <a name="datepickertextbox-states"></a>DatePickerTextBox 状态  
 下表列出了的可视状态<xref:System.Windows.Controls.Primitives.DatePickerTextBox>控件。  
  
|VisualState 名称|VisualStateGroup 名称|描述|  
|-|-|-|  
|普通|CommonStates|默认状态。|  
|已禁用|CommonStates|<xref:System.Windows.Controls.Primitives.DatePickerTextBox>被禁用。|  
|MouseOver|CommonStates|鼠标指针置于<xref:System.Windows.Controls.Primitives.DatePickerTextBox>。|  
|ReadOnly|CommonStates|用户不能更改中的文本<xref:System.Windows.Controls.Primitives.DatePickerTextBox>。|  
|已设定焦点|FocusStates|控件有焦点。|  
|失去焦点|FocusStates|控件没有焦点。|  
|打|WatermarkStates|该控件显示其初始文本。  <xref:System.Windows.Controls.Primitives.DatePickerTextBox>处于状态，当用户不具有输入文本或选择了日期。|  
|Unwatermarked|WatermarkStates|用户输入文本<xref:System.Windows.Controls.Primitives.DatePickerTextBox>中选择了日期或<xref:System.Windows.Controls.DatePicker>。|  
|有效|ValidationStates|该控件使用<xref:System.Windows.Controls.Validation>类和<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType>附加的属性是`false`。|  
|InvalidFocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType>附加的属性是`true`已在控件有焦点。|  
|InvalidUnfocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType>附加的属性是`true`具有该控件没有焦点。|  
  
## <a name="datepicker-controltemplate-example"></a>DatePicker ControlTemplate 示例  
 下面的示例演示如何定义<xref:System.Windows.Controls.ControlTemplate>为<xref:System.Windows.Controls.DatePicker>控件。  
  
 [!code-xaml[ControlTemplateExamples#DatePicker](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/datepicker.xaml#datepicker)]  
  
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
