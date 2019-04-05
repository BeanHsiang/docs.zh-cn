---
title: 用户描述的控件
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- custom controls [Windows Forms], user-drawn
- OnPaint method [Windows Forms]
- user-drawn controls [Windows Forms]
ms.assetid: 034af4b5-457f-4160-a937-22891817faa8
ms.openlocfilehash: 1529d4d62004becca4495d96fa893da20caa3954
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57709667"
---
# <a name="user-drawn-controls"></a>用户描述的控件
.NET Framework 为您提供了轻松开发自己的控件的功能。 可以创建一个用户控件，这是一组标准控件绑定到一起的代码，或您可以设计自己的控件的基础知识，设置。 甚至可以使用继承创建继承自现有控件的控件并将添加到其固有的功能。 无论何种方法使用，.NET Framework 提供了用于绘制用于您创建的任何控件的自定义图形界面的功能。  
  
 控件的绘制通过在控件的代码执行来实现<xref:System.Windows.Forms.Control.OnPaint%2A>方法。 单个参数的<xref:System.Windows.Forms.Control.OnPaint%2A>方法是<xref:System.Windows.Forms.PaintEventArgs>对象，它提供的所有信息和呈现控件所需的功能。 <xref:System.Windows.Forms.PaintEventArgs>作为属性提供了将控件的呈现中使用的两个主要对象：  
  
-   <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> 对象的矩形，表示要绘制的控件的一部分。 这可以是整个控件或具体取决于如何绘制控件的控件的一部分。  
  
-   <xref:System.Drawing.Graphics> 对象-封装一些面向图形的对象和提供必要的功能，绘制控件的方法。  
  
 有关详细信息<xref:System.Drawing.Graphics>对象以及如何使用它，请参阅[如何：创建用于绘制图形对象](../advanced/how-to-create-graphics-objects-for-drawing.md)。  
  
 <xref:System.Windows.Forms.Control.OnPaint%2A>每当绘制或在屏幕上，刷新控件触发事件和<xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A>对象表示在其中绘制会发生的矩形。 如果整个控件需要刷新，<xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A>将表示整个控件的大小。 如果只有一部分的控件需要刷新，但是，<xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A>对象将表示仅在需要重绘的区域。 这种情况的示例将在另一个控件或窗体用户界面中的部分已遮住控件时。  
  
 从继承时<xref:System.Windows.Forms.Control>类，必须重写<xref:System.Windows.Forms.Control.OnPaint%2A>方法并提供图形呈现代码中的。 如果你想要提供到用户控件或继承的控件的自定义图形界面，您可以也会这样通过重写<xref:System.Windows.Forms.Control.OnPaint%2A>方法。 示例如下所示：  
  
```vb  
Protected Overrides Sub OnPaint(ByVal e As PaintEventArgs)  
   ' Call the OnPaint method of the base class.  
   MyBase.OnPaint(e)  
  
   ' Declare and instantiate a drawing pen.  
   Using myPen As System.Drawing.Pen = New System.Drawing.Pen(Color.Aqua)  
      ' Draw an aqua rectangle in the rectangle represented by the control.  
      e.Graphics.DrawRectangle(myPen, New Rectangle(Me.Location, Me.Size))  
   End Using
End Sub  
```  
  
```csharp  
protected override void OnPaint(PaintEventArgs e)  
{  
   // Call the OnPaint method of the base class.  
   base.OnPaint(e);  
  
   // Declare and instantiate a new pen.  
   using (System.Drawing.Pen myPen = new System.Drawing.Pen(Color.Aqua))  
   {
      // Draw an aqua rectangle in the rectangle represented by the control.  
      e.Graphics.DrawRectangle(myPen, new Rectangle(this.Location,   
         this.Size));  
   }
}  
```  
  
 前面的示例演示如何呈现控件的非常简单的图形表示形式。 它将调用<xref:System.Windows.Forms.Control.OnPaint%2A>基类的方法，它创建<xref:System.Drawing.Pen>对象用来绘制，并绘制一个椭圆的矩形中由最后<xref:System.Windows.Forms.Control.Location%2A>和<xref:System.Windows.Forms.Control.Size%2A>的控件。 尽管大多数呈现代码都要比这更复杂，但此示例演示如何使用<xref:System.Drawing.Graphics>中包含对象<xref:System.Windows.Forms.PaintEventArgs>对象。 请注意，如果从已有的图形表示形式，例如一个类继承<xref:System.Windows.Forms.UserControl>或<xref:System.Windows.Forms.Button>，并不希望将该表示形式合并到您呈现，不应调用基类的<xref:System.Windows.Forms.Control.OnPaint%2A>方法。  
  
 中的代码<xref:System.Windows.Forms.Control.OnPaint%2A>控件的方法将执行迁移时首次绘制控件，或每当刷新。 若要确保每次调整大小，重绘控件，请将下行添加到您的控件的构造函数：  
  
```vb  
SetStyle(ControlStyles.ResizeRedraw, True)  
```  
  
```csharp  
SetStyle(ControlStyles.ResizeRedraw, true);  
```  
  
> [!NOTE]
>  使用<xref:System.Windows.Forms.Control.Region%2A?displayProperty=nameWithType>属性用于实现非矩形控件。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.Control.Region%2A>
- <xref:System.Windows.Forms.ControlStyles>
- <xref:System.Drawing.Graphics>
- <xref:System.Windows.Forms.Control.OnPaint%2A>
- <xref:System.Windows.Forms.PaintEventArgs>
- [如何：创建用于绘制图形对象](../advanced/how-to-create-graphics-objects-for-drawing.md)
- [构成控件](constituent-controls.md)
- [各种自定义控件](varieties-of-custom-controls.md)
