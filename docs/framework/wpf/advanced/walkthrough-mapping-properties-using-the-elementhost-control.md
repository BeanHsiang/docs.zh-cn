---
title: 演练：使用 ElementHost 控件映射属性
ms.date: 08/18/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- mapping properties [WPF]
- ElementHost control [WPF], mapping properties
ms.assetid: bccd6e0d-2272-4924-9107-ff8ed58b88aa
ms.openlocfilehash: 3fe3f00950fdfdf92c3f95dc42b27cc9110e0c95
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57371679"
---
# <a name="walkthrough-mapping-properties-using-the-elementhost-control"></a>演练：使用 ElementHost 控件映射属性

本演练演示如何使用<xref:System.Windows.Forms.Integration.ElementHost.PropertyMap%2A>属性将映射[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]属性设置为上托管的相应属性[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]元素。

本演练涉及以下任务：

-   创建项目。

-   定义新的属性映射。

-   删除默认属性映射。

-   扩展默认属性映射。

在本演练中所涉及任务的完整代码列表，请参阅[映射属性使用 ElementHost 控件示例](https://go.microsoft.com/fwlink/?LinkID=160018)。

完成后，你将能够映射[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]相对应的属性[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]上承载的元素的属性。

## <a name="prerequisites"></a>系统必备

你需要以下组件来完成本演练：

-   Visual Studio 2017

## <a name="creating-the-project"></a>创建项目

### <a name="to-create-the-project"></a>要创建项目

1.  创建**Windows 窗体应用程序**名为项目`PropertyMappingWithElementHost`。

2.  在中**解决方案资源管理器**，将引用添加到以下[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]程序集。

    -   PresentationCore

    -   PresentationFramework

    -   WindowsBase

    -   WindowsFormsIntegration

3.  将以下代码复制到顶部`Form1`代码文件。

     [!code-csharp[PropertyMappingWithElementHost#10](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#10)]
     [!code-vb[PropertyMappingWithElementHost#10](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#10)]

4.  在 Windows 窗体设计器中打开 `Form1`。 双击要添加的事件处理程序的窗体<xref:System.Windows.Forms.Form.Load>事件。

5.  返回到 Windows 窗体设计器并添加事件处理程序的窗体的<xref:System.Windows.Forms.Control.Resize>事件。 有关详细信息，请参阅[如何：创建事件处理程序使用设计器](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/zwwsdtbk(v=vs.100))。

6.  声明<xref:System.Windows.Forms.Integration.ElementHost>字段中`Form1`类。

     [!code-csharp[PropertyMappingWithElementHost#16](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#16)]
     [!code-vb[PropertyMappingWithElementHost#16](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#16)]

## <a name="defining-new-property-mappings"></a>定义新的属性映射

<xref:System.Windows.Forms.Integration.ElementHost>控件提供了一些默认属性映射。 通过调用添加新的属性映射<xref:System.Windows.Forms.Integration.PropertyMap.Add%2A>方法<xref:System.Windows.Forms.Integration.ElementHost>控件的<xref:System.Windows.Forms.Integration.ElementHost.PropertyMap%2A>。

### <a name="to-define-new-property-mappings"></a>若要定义新属性映射

1.  将以下代码复制到用于定义`Form1`类。

     [!code-csharp[PropertyMappingWithElementHost#12](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#12)]
     [!code-vb[PropertyMappingWithElementHost#12](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#12)]

     `AddMarginMapping`方法将添加的新映射<xref:System.Windows.Forms.Control.Margin%2A>属性。

     `OnMarginChange`方法将转换<xref:System.Windows.Forms.Control.Margin%2A>属性设置为[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]<xref:System.Windows.FrameworkElement.Margin%2A>属性。

2.  将以下代码复制到用于定义`Form1`类。

     [!code-csharp[PropertyMappingWithElementHost#14](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#14)]
     [!code-vb[PropertyMappingWithElementHost#14](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#14)]

     `AddRegionMapping`方法将添加的新映射<xref:System.Windows.Forms.Control.Region%2A>属性。

     `OnRegionChange`方法将转换<xref:System.Windows.Forms.Control.Region%2A>属性设置为[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]<xref:System.Windows.UIElement.Clip%2A>属性。

     `Form1_Resize`方法将处理窗体的<xref:System.Windows.Forms.Control.Resize>事件并调整其大小以适合所承载的元素的剪辑区域。

## <a name="removing-a-default-property-mapping"></a>删除默认属性映射

通过调用来移除默认属性映射<xref:System.Windows.Forms.Integration.PropertyMap.Remove%2A>方法<xref:System.Windows.Forms.Integration.ElementHost>控件的<xref:System.Windows.Forms.Integration.ElementHost.PropertyMap%2A>。

### <a name="to-remove-a-default-property-mapping"></a>删除默认属性映射

-   将以下代码复制到用于定义`Form1`类。

     [!code-csharp[PropertyMappingWithElementHost#13](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#13)]
     [!code-vb[PropertyMappingWithElementHost#13](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#13)]

     `RemoveCursorMapping`方法删除默认映射<xref:System.Windows.Forms.Control.Cursor%2A>属性。

## <a name="extending-a-default-property-mapping"></a>扩展默认属性映射

可以使用默认属性映射，并使用自己的映射对其进行扩展。

### <a name="to-extend-a-default-property-mapping"></a>扩展默认属性映射

-   将以下代码复制到用于定义`Form1`类。

     [!code-csharp[PropertyMappingWithElementHost#15](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#15)]
     [!code-vb[PropertyMappingWithElementHost#15](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#15)]

     `ExtendBackColorMapping`方法将自定义属性转换器添加到现有<xref:System.Windows.Forms.Control.BackColor%2A>属性映射。

     `OnBackColorChange`方法将特定图像分配给托管控件的<xref:System.Windows.Controls.Control.Background%2A>属性。 `OnBackColorChange`应用默认属性映射后调用方法。

## <a name="initialize-your-property-mappings"></a>初始化属性映射

1.  将以下代码复制到用于定义`Form1`类。

     [!code-csharp[PropertyMappingWithElementHost#11](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#11)]
     [!code-vb[PropertyMappingWithElementHost#11](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#11)]

     `Form1_Load`方法将处理<xref:System.Windows.Forms.Form.Load>事件并执行以下初始化。

    -   创建[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]<xref:System.Windows.Controls.Button>元素。

    -   调用先前在演练中定义的方法来设置属性映射。

    -   将初始值分配给映射的属性。

2.  按 F5 生成并运行该应用程序。

## <a name="see-also"></a>请参阅

- <xref:System.Windows.Forms.Integration.ElementHost.PropertyMap%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost.PropertyMap%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [Windows 窗体和 WPF 属性映射](windows-forms-and-wpf-property-mapping.md)
- [在 Visual Studio 中设计 XAML](/visualstudio/designers/designing-xaml-in-visual-studio)
- [演练：承载 WPF 复合控件在 Windows 窗体中](walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)