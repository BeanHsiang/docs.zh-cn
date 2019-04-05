---
title: 如何：实现绑定验证
ms.date: 03/30/2017
helpviewer_keywords:
- validation of binding [WPF]
- data binding [WPF], validation of binding
- binding [WPF], validation of
ms.assetid: eb98b33d-9866-49ae-b981-bc5ff20d607a
ms.openlocfilehash: eefdb3b1205a64221e3e9352f70e3d06dc074eff
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57368540"
---
# <a name="how-to-implement-binding-validation"></a>如何：实现绑定验证
此示例演示如何在用户输入无效值后，基于自定义验证规则使用 <xref:System.Windows.Controls.Validation.ErrorTemplate%2A> 和样式触发器来提供视觉反馈，以便通知用户。  
  
## <a name="example"></a>示例  
 在下面的示例中，<xref:System.Windows.Controls.TextBox> 的文本内容绑定到一个名为 `ods` 的绑定源对象的 `Age` 属性（类型为 int) 。 该绑定已设置为使用名为 `AgeRangeRule` 的验证规则。因此，当用户输入了非数值字符或输入的值小于 21 或者大于 130 时，文本框旁边会显示一个红色感叹号，而当用户将鼠标移动到该文本框上时，会显示包含错误消息的工具提示。  
  
 [!code-xaml[BindValidation#2](~/samples/snippets/csharp/VS_Snippets_Wpf/BindValidation/CSharp/Window1.xaml#2)]  
  
 下面的示例演示如何实现 `AgeRangeRule`，它继承 <xref:System.Windows.Controls.ValidationRule> 并重写 <xref:System.Windows.Controls.ValidationRule.Validate%2A> 方法。 对值调用 Int32.Parse() 方法是为了确保该值不包含任何无效字符。 <xref:System.Windows.Controls.ValidationRule.Validate%2A> 方法将返回 <xref:System.Windows.Controls.ValidationResult>，该返回结果指示值是否有效（根据是否在分析期间捕获了异常，以及年龄值是否超出了下限和上限）。  
  
 [!code-csharp[BindValidation#3](~/samples/snippets/csharp/VS_Snippets_Wpf/BindValidation/CSharp/AgeRangeRule.cs#3)]  
  
 下面的示例演示了自定义 <xref:System.Windows.Controls.ControlTemplate> `validationTemplate`，后者会创建一个红色感叹号来通知用户存在验证错误。 控件模板用于重新定义控件的外观。  
  
 [!code-xaml[BindValidation#4](~/samples/snippets/csharp/VS_Snippets_Wpf/BindValidation/CSharp/Window1.xaml#4)]  
  
 如以下示例所示，显示错误消息的 <xref:System.Windows.Controls.ToolTip> 是通过名为 `textBoxInError` 的样式创建的。 如果 <xref:System.Windows.Controls.Validation.HasError%2A> 的值是 `true`，该触发器会将当前 <xref:System.Windows.Controls.TextBox> 的工具提示设置为其第一个验证错误。 <xref:System.Windows.Data.Binding.RelativeSource%2A> 设置为 <xref:System.Windows.Data.RelativeSourceMode.Self>，用于引用当前元素。  
  
 [!code-xaml[BindValidation#5](~/samples/snippets/csharp/VS_Snippets_Wpf/BindValidation/CSharp/Window1.xaml#5)]  
  
 有关完整示例，请参阅[绑定验证示例](https://go.microsoft.com/fwlink/?LinkID=159972)。  
  
 请注意，如果未提供自定义 <xref:System.Windows.Controls.Validation.ErrorTemplate%2A>，则当验证出错时,系统会使用默认错误模板向用户提供可视反馈。 有关详细信息，请参阅[数据绑定概述](data-binding-overview.md)中的“数据验证”。 另外，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 还提供了内置验证规则，该规则捕获在更新绑定源属性期间引发的异常。 有关详细信息，请参阅 <xref:System.Windows.Controls.ExceptionValidationRule>。  
  
## <a name="see-also"></a>请参阅
- [数据绑定概述](data-binding-overview.md)
- [帮助主题](data-binding-how-to-topics.md)
