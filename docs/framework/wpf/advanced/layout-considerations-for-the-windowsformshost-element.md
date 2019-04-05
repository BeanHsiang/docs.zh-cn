---
title: WindowsFormsHost 元素的布局注意事项
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms [WPF], interoperability with
- Windows Forms [WPF], WPF interoperation
- interoperability [WPF], Windows Forms
- WindowsFormsHost element layout considerations [WPF]
- dynamic layout [WPF interoperability]
- device-independent pixels
ms.assetid: 3c574597-bbde-440f-95cc-01371f1a5d9d
ms.openlocfilehash: 891254ff44926a719bb0c124e5dc098fd3f3e82e
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57366538"
---
# <a name="layout-considerations-for-the-windowsformshost-element"></a>WindowsFormsHost 元素的布局注意事项
本主题介绍如何<xref:System.Windows.Forms.Integration.WindowsFormsHost>与元素交互[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]布局系统。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 和[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]支持不同，但类似的逻辑大小和位置上窗体或页面的元素。 当你创建混合用户界面 (UI) 承载[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]中的控件[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]，则<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素集成这两种布局方案。  
  
## <a name="differences-in-layout-between-wpf-and-windows-forms"></a>在布局中 WPF 和 Windows 窗体之间的差异  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 使用独立于分辨率的布局。 所有[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]使用指定的布局维度*设备无关的像素*。 独立于设备的像素是一个 96 英寸为单位的大小和分辨率无关的因此获得相似的结果，而不考虑呈现到 72 dpi 监视器或 19200 dpi 打印机。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 也基于*动态布局*。 这意味着 UI 元素会在窗体或根据其内容，其父级的布局容器，并可用的屏幕大小的页面上排列本身。 动态布局可简化本地化过程，它们包含的字符串长度更改时自动调整大小和 UI 元素的位置。  
  
 中的布局[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]是依赖于设备的和更有可能是静态的。 通常情况下，[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件在窗体使用硬件以像素为单位指定的维度上采用绝对定位。 但是，[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]支持某些动态布局功能，如下表中进行了总结。  
  
|布局功能|描述|  
|--------------------|-----------------|  
|自动调整大小|某些[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件调整自身大小以正确显示其内容。 有关详细信息，请参阅[AutoSize 属性概述](../../winforms/controls/autosize-property-overview.md)。|  
|锚定和停靠|[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 控件支持调整位置和大小基于父容器。 有关详细信息，请参阅 <xref:System.Windows.Forms.Control.Anchor%2A?displayProperty=nameWithType> 和 <xref:System.Windows.Forms.Control.Dock%2A?displayProperty=nameWithType>。|  
|自动缩放|容器控件来调整自身及其子级的输出设备或大小，以像素为单位的默认容器字体的分辨率。 有关详细信息，请参阅[在 Windows 窗体中的自动缩放](../../winforms/automatic-scaling-in-windows-forms.md)。|  
|布局容器|<xref:System.Windows.Forms.FlowLayoutPanel>和<xref:System.Windows.Forms.TableLayoutPanel>控件排列其子控件和调整自身大小根据其内容。|  
  
## <a name="layout-limitations"></a>布局的限制  
 一般情况下，[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件不能缩放和转换中可能的范围为[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]。 以下列表描述了已知的限制时<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素尝试将其承载[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控制[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]布局系统。  
  
-   某些情况下，不能调整 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 控件的大小，或者大小只能调整为特定尺寸。 例如， [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] <xref:System.Windows.Forms.ComboBox>控件支持仅的单一高度由控件的字体大小定义。 在中[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]其中元素可以垂直拉伸，托管的动态布局<xref:System.Windows.Forms.ComboBox>控件不会按预期方式拉伸。  
  
-   不能旋转或扭曲 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 控件。 <xref:System.Windows.Forms.Integration.WindowsFormsHost>元素将引发<xref:System.Windows.Forms.Integration.WindowsFormsHost.LayoutError>事件，如果应用倾斜或旋转转换。 如果不处理<xref:System.Windows.Forms.Integration.WindowsFormsHost.LayoutError>事件，<xref:System.InvalidOperationException>引发。  
  
-   大多数情况下，[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 控件不支持按比例缩放。 尽管该控件的整体尺寸将会缩放，但其子控件和组件元素可能不会按预期调整大小。 此限制取决于每个 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 控件支持缩放的程度。 此外，不能缩放[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]缩小到 0 像素的大小的控件。  
  
-   [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 控件支持自动缩放，在其中窗体将自动调整大小本身和它基于字体大小的控件。 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 用户界面中，更改字号不会改变整个布局的大小，但是可动态调整单个元素的大小。  
  
### <a name="z-order"></a>Z 顺序  
 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 用户界面中，可以更改元素的 z 顺序以控制重叠行为。 由于承载的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 控件是在单独的 HWND 中绘制的，所以始终在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 元素之上绘制它。  
  
 一个承载[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]还在任何之上绘制控件<xref:System.Windows.Documents.Adorner>元素。  
  
## <a name="layout-behavior"></a>布局行为  
 托管时，以下部分介绍的布局行为的特定方面[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]中的控件[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]。  
  
### <a name="scaling-unit-conversion-and-device-independence"></a>缩放、 单位换算和设备独立性  
 每当<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素执行操作涉及[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]和[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]涉及维度，两个坐标系统： 独立于设备的像素[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]和硬件像素[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]。 因此，你必须应用适当的单位和缩放转换，以实现一致的布局。  
  
 坐标系统之间的转换取决于当前的设备分辨率和任何布局或呈现转换应用于<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素或对其的上级。  
  
 如果输出设备为 96 dpi，无需进行扩展已应用到<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素中，一个独立于设备的像素是否等于一个硬件像素。  
  
 所有其他情况下需要缩放坐标系统。 不调整承载的控件的大小。 相反，<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素尝试缩放承载的控件及其所有子控件。 因为[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]不完全支持缩放，<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素可以扩展到由特定控件支持的程度。  
  
 重写<xref:System.Windows.Forms.Integration.WindowsFormsHost.ScaleChild%2A>方法以提供自定义的缩放行为的托管 Windows 窗体控件。  
  
 除了缩放以外，<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素处理舍入和溢出的情况下下, 表中所述。  
  
|转换问题|描述|  
|----------------------|-----------------|  
|舍入|[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 指定为独立于设备的像素尺寸`double`，并[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]硬件像素大小指定为`int`。 在情况下， `double`-基于的维度转换为`int`-基于维度，<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素使用标准的舍入，以便小于 0.5 的小数部分的值是向下舍入为 0。|  
|溢出|当<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素将从转换`double`值到`int`值，可能会溢出。 值大于<xref:System.Int32.MaxValue>设置为<xref:System.Int32.MaxValue>。|  
  
### <a name="layout-related-properties"></a>与布局相关的属性  
 控制中的布局行为的属性[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件和[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]相应地通过映射元素<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素。 有关详细信息，请参阅 [Windows 窗体和 WPF 属性映射](windows-forms-and-wpf-property-mapping.md)。  
  
### <a name="layout-changes-in-the-hosted-control"></a>托管控件中的布局更改  
 中托管的布局更改[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件将传播到[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]以触发布局更新。 <xref:System.Windows.UIElement.InvalidateMeasure%2A>方法<xref:System.Windows.Forms.Integration.WindowsFormsHost>可确保在承载控件的布局更改会造成[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]布局引擎来运行。  
  
### <a name="continuously-sized-windows-forms-controls"></a>持续调整 Windows 窗体控件  
 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 与支持连续缩放完全的控件进行交互[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]布局系统。 <xref:System.Windows.Forms.Integration.WindowsFormsHost>元素使用<xref:System.Windows.FrameworkElement.MeasureOverride%2A>并<xref:System.Windows.FrameworkElement.ArrangeOverride%2A>方法，像往常一样来调整和排列承载[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件。  
  
### <a name="sizing-algorithm"></a>调整大小算法  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>元素使用以下过程来托管的控件的大小：  
  
1.  <xref:System.Windows.Forms.Integration.WindowsFormsHost>元素会替代<xref:System.Windows.FrameworkElement.MeasureOverride%2A>和<xref:System.Windows.FrameworkElement.ArrangeOverride%2A>方法。  
  
2.  若要确定所承载控件的大小<xref:System.Windows.FrameworkElement.MeasureOverride%2A>方法调用托管的控件的<xref:System.Windows.Forms.Control.GetPreferredSize%2A>方法使用约束转换从传递给约束<xref:System.Windows.FrameworkElement.MeasureOverride%2A>方法。  
  
3.  <xref:System.Windows.FrameworkElement.ArrangeOverride%2A>方法会尝试将所承载的控件设置为给定的大小约束。  
  
4.  如果托管的控件的<xref:System.Windows.Forms.Control.Size%2A>属性进行匹配指定的约束时，所承载的控件的大小为该约束。  
  
 如果<xref:System.Windows.Forms.Control.Size%2A>属性与指定的约束不匹配，所承载的控件不支持连续的大小调整。 例如，<xref:System.Windows.Forms.MonthCalendar>控件允许连续的大小。 此控件的允许的大小包含高度和宽度的整数 （表示的月数）。 中，这种情况下<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素的行为，如下所示：  
  
-   如果<xref:System.Windows.Forms.Control.Size%2A>属性返回与指定的约束，更大的大小<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素剪辑所承载的控件。 高度和宽度是分别进行处理，因此可能在任一方向剪辑所承载的控件。  
  
-   如果<xref:System.Windows.Forms.Control.Size%2A>属性返回与指定的约束，较小的大小<xref:System.Windows.Forms.Integration.WindowsFormsHost>接受此大小值并返回到值[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]布局系统。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [演练：在 WPF 中排列 Windows 窗体控件](walkthrough-arranging-windows-forms-controls-in-wpf.md)
- [在 WPF 示例中排列 Windows 窗体控件](https://go.microsoft.com/fwlink/?LinkID=159971)
- [Windows 窗体和 WPF 属性映射](windows-forms-and-wpf-property-mapping.md)
- [迁移和互操作性](migration-and-interoperability.md)
