---
title: 如何：创建显示进度的 Windows 窗体控件
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [Windows Forms], progress tracking
- controls [Windows Forms], creating
- progress [Windows Forms], reporting [Windows Forms]
- FlashTrackBar custom control
ms.assetid: 24c5a2e3-058c-4b8d-a217-c06e6a130c2f
ms.openlocfilehash: 6910a7e2e68a3807e08a8b196dde003e1d5bc9af
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57720235"
---
# <a name="how-to-create-a-windows-forms-control-that-shows-progress"></a>如何：创建显示进度的 Windows 窗体控件
以下代码示例显示了一个名为 `FlashTrackBar` 的自定义控件，可用于向用户显示应用程序的级别或进度。 它使用渐变来直观地表示进度。  
  
 `FlashTrackBar` 控件阐释了以下概念：  
  
-   定义自定义属性。  
  
-   定义自定义事件。 （`FlashTrackBar` 定义 `ValueChanged` 事件。）  
  
-   重写<xref:System.Windows.Forms.Control.OnPaint%2A>方法以提供绘制控件的逻辑。  
  
-   计算可用于绘制控件使用的区域及其<xref:System.Windows.Forms.Control.ClientRectangle%2A>属性。 `FlashTrackBar` 在 `OptimizedInvalidate` 方法中执行此操作。  
  
-   在 Windows 窗体设计器中更改属性时，实现其序列化或持久性。 `FlashTrackBar` 定义用于序列化其 `StartColor` 和 `EndColor` 属性的 `ShouldSerializeStartColor` 和 `ShouldSerializeEndColor` 方法。  
  
 下表显示了由 `FlashTrackBar` 定义的自定义属性。  
  
|属性|描述|  
|--------------|-----------------|  
|`AllowUserEdit`|指示用户是否可以通过单击和拖动来更改闪存跟踪条的值。|  
|`EndColor`|指定跟踪条的结束颜色。|  
|`DarkenBy`|指定相对于前景渐变加深背景颜色的程度。|  
|`Max`|指定跟踪条的最大值。|  
|`Min`|指定跟踪条的最小值。|  
|`StartColor`|指定渐变的开始颜色。|  
|`ShowPercentage`|指示是否在渐变上显示百分比。|  
|`ShowValue`|指示是否在渐变上显示当前值。|  
|`ShowGradient`|指示跟踪条是否应显示有当前值的颜色渐变。|  
|-   `Value`|指定跟踪条的当前值。|  
  
 下表显示了 `FlashTrackBar:` 定义的其他成员：property-changed 事件和引发该事件的方法。  
  
|成员|描述|  
|------------|-----------------|  
|`ValueChanged`|当跟踪条的 `Value` 属性更改时引发的事件。|  
|`OnValueChanged`|引发 `ValueChanged` 事件的方法。|  
  
> [!NOTE]
>  `FlashTrackBar` 使用<xref:System.EventArgs>的事件数据类和<xref:System.EventHandler>事件委托。  
  
 若要处理相应*EventName*事件`FlashTrackBar`重写它所继承的以下方法<xref:System.Windows.Forms.Control?displayProperty=nameWithType>:  
  
-   <xref:System.Windows.Forms.Control.OnPaint%2A>  
  
-   <xref:System.Windows.Forms.Control.OnMouseDown%2A>  
  
-   <xref:System.Windows.Forms.Control.OnMouseMove%2A>  
  
-   <xref:System.Windows.Forms.Control.OnMouseUp%2A>  
  
-   <xref:System.Windows.Forms.Control.OnResize%2A>  
  
 若要处理相应的 property-changed 事件`FlashTrackBar`重写它所继承的以下方法<xref:System.Windows.Forms.Control?displayProperty=nameWithType>:  
  
-   <xref:System.Windows.Forms.Control.OnBackColorChanged%2A>  
  
-   <xref:System.Windows.Forms.Control.OnBackgroundImageChanged%2A>  
  
-   <xref:System.Windows.Forms.Control.OnTextChanged%2A>  
  
## <a name="example"></a>示例  
 `FlashTrackBar` 控件定义了两个 UI 类型编辑器（`FlashTrackBarValueEditor` 和 `FlashTrackBarDarkenByEditor`），它们显示在以下代码列表中。 `HostApp` 类在 Windows 窗体上使用 `FlashTrackBar` 控件。  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBar.cs#1)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBar.vb#1)]  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#10](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBarDarkenByEditor.cs#10)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBarDarkenByEditor.vb#10)]  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#20](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBarValueEditor.cs#20)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#20](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBarValueEditor.vb#20)]  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#30](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/HostApp.cs#30)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#30](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/HostApp.vb#30)]  
  
## <a name="see-also"></a>请参阅
- [扩展设计时支持](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/37899azc(v=vs.120))
- [Windows 窗体控件开发基础知识](windows-forms-control-development-basics.md)
