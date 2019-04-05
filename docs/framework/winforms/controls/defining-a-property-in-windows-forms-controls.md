---
title: 在 Windows 窗体控件中定义属性
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- properties [Windows Forms], defining in code
- custom controls [Windows Forms], defining properties in code
ms.assetid: c2eb8277-a842-4d99-89a9-647b901a0434
ms.openlocfilehash: 84273d2fab36df287eaca70f5f32fd8024a9204d
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57712196"
---
# <a name="defining-a-property-in-windows-forms-controls"></a>在 Windows 窗体控件中定义属性
有关属性的概述，请参阅[属性概述](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/65zdfbdt(v=vs.120))。 定义属性时需考虑以下重要注意事项：  
  
-   必须将特性应用于定义的属性。 特性指定设计器应如何显示属性。 有关详细信息，请参阅[组件的设计时特性](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/tk67c2t8(v=vs.120))。  
  
-   如果更改该属性会影响该控件的可视显示，则调用<xref:System.Windows.Forms.Control.Invalidate%2A>方法 (继承自控件<xref:System.Windows.Forms.Control>) 从`set`访问器。 <xref:System.Windows.Forms.Control.Invalidate%2A> 反过来调用<xref:System.Windows.Forms.Control.OnPaint%2A>方法，重绘控件。 多次调用<xref:System.Windows.Forms.Control.Invalidate%2A>导致调用一次<xref:System.Windows.Forms.Control.OnPaint%2A>以提高效率。  
  
-   .NET Framework 类库为常见数据类型（如整数、小数、布尔值和其他数据类型）提供了类型转换器。 类型转换器的用途通常是提供字符串到数值的转换（从字符串数据转换为其他数据类型）。 常见数据类型与默认类型转换器相关联，默认类型转换器可将数值转换为字符串，并将字符串转换为相应数据类型。 如果定义了自定义（即非标准）数据类型的属性，则应用的特性必须将类型转换器指定为与该属性相关联。 还可使用特性将自定义 UI 类型编辑器与某个属性相关联。 UI 类型编辑器提供一个用于编辑属性或数据类型的用户界面。 UI 类型编辑器的一个例子是颜色选取器。 本主题末尾给出了特性的示例。  
  
    > [!NOTE]
    >  如果没有类型转换器或 UI 类型编辑器可供自定义属性使用，则可根据[扩展设计时支持](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/37899azc(v=vs.120))中所述来实现一个。  
  
 以下代码片段为自定义控件 `FlashTrackBar` 定义了一个名为 `EndColor` 的自定义属性。  
  
```vb  
Public Class FlashTrackBar  
   Inherits Control  
   ...  
   ' Private data member that backs the EndColor property.  
   Private _endColor As Color = Color.LimeGreen  
  
   ' The Category attribute tells the designer to display  
   ' it in the Flash grouping.   
   ' The Description attribute provides a description of  
   ' the property.   
   <Category("Flash"), _  
   Description("The ending color of the bar.")>  _  
   Public Property EndColor() As Color  
      ' The public property EndColor accesses _endColor.  
      Get  
         Return _endColor  
      End Get  
      Set  
         _endColor = value  
         If Not (baseBackground Is Nothing) And showGradient Then  
            baseBackground.Dispose()  
            baseBackground = Nothing  
         End If  
         ' The Invalidate method calls the OnPaint method, which redraws    
         ' the control.  
         Invalidate()  
      End Set  
   End Property  
   ...  
End Class  
```  
  
```csharp  
public class FlashTrackBar : Control {  
   ...  
   // Private data member that backs the EndColor property.  
   private Color endColor = Color.LimeGreen;  
   // The Category attribute tells the designer to display  
   // it in the Flash grouping.   
   // The Description attribute provides a description of  
   // the property.   
   [  
   Category("Flash"),  
   Description("The ending color of the bar.")  
   ]  
   // The public property EndColor accesses endColor.  
   public Color EndColor {  
      get {  
         return endColor;  
      }  
      set {  
         endColor = value;  
         if (baseBackground != null && showGradient) {  
            baseBackground.Dispose();  
            baseBackground = null;  
         }  
         // The Invalidate method calls the OnPaint method, which redraws   
         // the control.  
         Invalidate();  
      }  
   }  
   ...  
}  
```  
  
 以下代码片段将类型转换器和 UI 类型编辑器与属性 `Value` 相关联。 在这种情况下`Value`是一个整数，具有默认类型转换器，但<xref:System.ComponentModel.TypeConverterAttribute>属性将应用自定义类型转换器 (`FlashTrackBarValueConverter`)，使设计器，以百分比形式显示。 UI 类型编辑器 `FlashTrackBarValueEditor` 允许以可视化方式显示百分比。 此示例还表明，类型转换器或编辑器由指定<xref:System.ComponentModel.TypeConverterAttribute>或<xref:System.ComponentModel.EditorAttribute>特性将重写默认转换器。  
  
```vb  
<Category("Flash"), _  
TypeConverter(GetType(FlashTrackBarValueConverter)), _  
Editor(GetType(FlashTrackBarValueEditor), _  
GetType(UITypeEditor)), _  
Description("The current value of the track bar.  You can enter an actual value or a percentage.")>  _  
Public ReadOnly Property Value() As Integer  
...  
End Property  
```  
  
```csharp  
[  
Category("Flash"),   
TypeConverter(typeof(FlashTrackBarValueConverter)),  
Editor(typeof(FlashTrackBarValueEditor), typeof(UITypeEditor)),  
Description("The current value of the track bar.  You can enter an actual value or a percentage.")  
]  
public int Value {  
...  
}  
```  
  
## <a name="see-also"></a>请参阅
- [Windows 窗体控件中的属性](properties-in-windows-forms-controls.md)
- [使用 ShouldSerialize 和 Reset 方法定义默认值](defining-default-values-with-the-shouldserialize-and-reset-methods.md)
- [属性更改事件](property-changed-events.md)
- [Windows 窗体控件中的特性](attributes-in-windows-forms-controls.md)
