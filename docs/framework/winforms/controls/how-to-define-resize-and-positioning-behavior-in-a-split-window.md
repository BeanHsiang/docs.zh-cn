---
title: 如何：定义大小调整和拆分窗口中定位行为
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- split windows [Windows Forms], resizing
- splitter windows [Windows Forms], resizing
- SplitContainer control [Windows Forms], resizing
ms.assetid: 9bf73f36-ed2d-4a02-b15a-0770eff4fdfa
ms.openlocfilehash: a0e16a1961e5eb7fcb81503d0ccead38e08974dc
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54628248"
---
# <a name="how-to-define-resize-and-positioning-behavior-in-a-split-window"></a>如何：定义大小调整和拆分窗口中定位行为
面板的<xref:System.Windows.Forms.SplitContainer>控件有助于使自身也要调整其大小和由用户操作。 但是，将有的时间时要以编程方式控制拆分器 — 其中其定位和可以移动的程度。  
  
 <xref:System.Windows.Forms.SplitContainer.SplitterIncrement%2A>属性和其他属性上的<xref:System.Windows.Forms.SplitContainer>控件使您的用户界面以满足你需求的行为的精确控制。 下表列出了这些属性。  
  
|name|描述|  
|----------|-----------------|  
|<xref:System.Windows.Forms.SplitContainer.IsSplitterFixed%2A> 属性|确定是否拆分器是可移动通过键盘或鼠标。|  
|<xref:System.Windows.Forms.SplitContainer.SplitterDistance%2A> 属性|确定在从左边缘或上边缘到可移动拆分条的像素的距离。|  
|<xref:System.Windows.Forms.SplitContainer.SplitterIncrement%2A> 属性|确定的最小距离，以像素为单位，用户可以移动拆分器。|  
  
 下面的示例修改<xref:System.Windows.Forms.SplitContainer.SplitterIncrement%2A>属性来创建"对齐拆分器"的效果; 当用户拖动拆分器，它都增加 10 个像素，而不是默认值 1 为单位。  
  
### <a name="to-define-splitcontainer-resize-behavior"></a>若要定义 SplitContainer 调整大小行为  
  
1.  在过程中，设置<xref:System.Windows.Forms.SplitContainer.SplitterIncrement%2A>属性设置为所需的大小，以便实现拆分器的对齐行为。  
  
     在以下代码示例中，在窗体内<xref:System.Windows.Forms.Form.Load>事件，在拆分器<xref:System.Windows.Forms.SplitContainer>控件被设置为 10 个像素拖动时跳转。  
  
    ```vb  
    Private Sub Form1_Load(ByVal sender As System.Object, _  
        ByVal e As System.EventArgs) Handles MyBase.Load  
        Dim splitSnapper as new SplitContainer()  
        splitSnapper.SplitterIncrement = 10  
        splitSnapper.Dock = DockStyle.Fill  
        splitSnapper.Parent = me  
    End Sub  
    ```  
  
    ```csharp  
    private void Form1_Load(System.Object sender, System.EventArgs e)  
    {  
        SplitContainer splitSnapper = new SplitContainer();  
        splitSnapper.SplitterIncrement = 10;  
        splitSnapper.Dock = DockStyle.Fill;  
        splitSnapper.Parent = this;  
    }  
    ```  
  
     (Visual C#)将以下代码放在窗体的构造函数中以注册事件处理程序。  
  
    ```csharp  
    this.Load += new System.EventHandler(this.Form1_Load);  
    ```  
  
     稍微向左或向右移动拆分器将具有无明显的效果;但是，当鼠标指针在任一方向的 10 个像素，拆分器将对齐到新位置。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.SplitContainer>
- <xref:System.Windows.Forms.SplitContainer.SplitterIncrement%2A>
