---
title: Windows 窗体控件中的特性
ms.date: 03/30/2017
helpviewer_keywords:
- attributes [Windows Forms]
- attributes [Windows Forms], data binding properties
- attributes [Windows Forms], control properties
- attributes [Windows Forms], classes
ms.assetid: 2c5640e9-6c6c-49d7-a5e4-a768f6be7853
ms.openlocfilehash: 8e845df7eb83f01adb2086025cf47e7fdc896ba6
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57724396"
---
# <a name="attributes-in-windows-forms-controls"></a>Windows 窗体控件中的特性
.NET Framework 提供了多种可应用于自定义控件和组件的成员的特性。 其中的一些特性会影响类的运行时行为，另一些会影响设计时行为。  
  
## <a name="attributes-for-control-and-component-properties"></a>控件和组件属性的特性  
 下表显示了可应用于自定义控件和组件的属性或其他成员的特性。 有关使用这些属性的许多示例，请参阅[如何：应用 Windows 窗体控件中的特性](how-to-apply-attributes-in-windows-forms-controls.md)。  
  
|特性|描述|  
|---------------|-----------------|  
|<xref:System.ComponentModel.AmbientValueAttribute>|指定要传递给属性的值，以使该属性从另一个源中获取其值。 这称为“环境”。|  
|<xref:System.ComponentModel.BrowsableAttribute>|指定属性或事件是否应在“属性”窗口中显示。|  
|<xref:System.ComponentModel.CategoryAttribute>|指定在其中进行分组的属性或事件时显示在类别的名称<xref:System.Windows.Forms.PropertyGrid>控件设置为<xref:System.Windows.Forms.PropertySort.Categorized>模式。|  
|<xref:System.ComponentModel.DefaultValueAttribute>|指定属性的默认值。|  
|<xref:System.ComponentModel.DescriptionAttribute>|指定属性或事件的说明。|  
|<xref:System.ComponentModel.DisplayNameAttribute>|为属性、事件或不采用参数的 `public void` 方法指定显示名称。|  
|<xref:System.ComponentModel.EditorAttribute>|指定用于更改属性的编辑器。|  
|<xref:System.ComponentModel.EditorBrowsableAttribute>|指定可在编辑器中查看的属性或方法。|  
|<xref:System.ComponentModel.Design.HelpKeywordAttribute>|指定类或成员的上下文关键字。|  
|<xref:System.ComponentModel.LocalizableAttribute>|指定是否应本地化某一属性。|  
|<xref:System.ComponentModel.PasswordPropertyTextAttribute>|指示对象的文本表示形式被星号等字符隐匿。|  
|<xref:System.ComponentModel.ReadOnlyAttribute>|指定此特性绑定到的属性在设计时是只读还是可读/写。|  
|<xref:System.ComponentModel.RefreshPropertiesAttribute>|指示关联的属性值更改时应刷新属性网格。|  
|<xref:System.ComponentModel.TypeConverterAttribute>|指定对于此属性绑定到的对象要使用哪种类型作为转换器。|  
  
## <a name="attributes-for-data-binding-properties"></a>数据绑定属性的特性  
 下表显示了可用于指定自定义控件和组件如何与数据绑定之间进行交互的特性。  
  
|特性|描述|  
|---------------|-----------------|  
|<xref:System.ComponentModel.BindableAttribute>|指定属性是否通常用于绑定。|  
|<xref:System.ComponentModel.ComplexBindingPropertiesAttribute>|指定组件的数据源和数据成员属性。|  
|<xref:System.ComponentModel.DefaultBindingPropertyAttribute>|指定组件的默认绑定属性。|  
|<xref:System.ComponentModel.LookupBindingPropertiesAttribute>|指定组件的数据源和数据成员属性。|  
|<xref:System.ComponentModel.AttributeProviderAttribute>|启用特性重定向。|  
  
## <a name="attributes-for-classes"></a>类的特性  
 下表显示了可用于在设计时指定自定义控件和组件的行为的特性。  
  
|特性|描述|  
|---------------|-----------------|  
|<xref:System.ComponentModel.DefaultEventAttribute>|指定组件的默认事件。|  
|<xref:System.ComponentModel.DefaultPropertyAttribute>|指定组件的默认属性。|  
|<xref:System.ComponentModel.DesignerAttribute>|指定用于为组件实现设计时服务的类。|  
|<xref:System.ComponentModel.DesignerCategoryAttribute>|指定类设计器属于某一类别。|  
|<xref:System.ComponentModel.ToolboxItemAttribute>|表示工具箱项的特性。|  
|<xref:System.ComponentModel.ToolboxItemFilterAttribute>|指定要用于工具箱项的筛选器字符串和筛选器类型。|  
  
## <a name="see-also"></a>请参阅
- <xref:System.Attribute>
- [如何：应用 Windows 窗体控件中的特性](how-to-apply-attributes-in-windows-forms-controls.md)
- [扩展设计时支持](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/37899azc(v=vs.120))
- [使用 .NET Framework 开发自定义 Windows 窗体控件](developing-custom-windows-forms-controls.md)
