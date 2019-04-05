---
title: 如何：从现有 Windows 窗体控件继承
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- inheritance [Windows Forms], Windows Forms custom controls
- custom controls [Windows Forms], inheritance
ms.assetid: 1e1fc8ea-c615-4cf0-a356-16d6df7444ab
ms.openlocfilehash: 9b3b5b2420a1121be81bc299dea645051f941cd8
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57707971"
---
# <a name="how-to-inherit-from-existing-windows-forms-controls"></a>如何：从现有 Windows 窗体控件继承
如果想要扩展现有控件的功能，可以通过继承创建一个派生自现有控件的控件。 从现有控件继承时，将继承该控件的的所有功能和可视属性。 例如，如果已创建的控件继承自<xref:System.Windows.Forms.Button>、 新控件看起来和 act 完全一样标准<xref:System.Windows.Forms.Button>控件。 然后可以通过实现自定义方法和属性来扩展或修改新控件的功能。 在某些控件中，您还可以更改继承的控件的可视外观通过重写其<xref:System.Windows.Forms.Control.OnPaint%2A>方法。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
### <a name="to-create-an-inherited-control"></a>创建继承的控件  
  
1.  创建新的 **Windows 窗体应用程序**项目。  
  
2.  从“项目”菜单中选择“添加新项”。  
  
     “添加新项”对话框随即出现。  
  
3.  在“添加新项”对话框中，双击“自定义控件”。  
  
     一个新的自定义控件将被添加到项目中。  
  
4.  如果使用的是 Visual Basic，则在“解决方案资源管理器”的顶部单击“显示所有文件”。 展开 CustomControl1.vb，然后在“代码编辑器”中打开 CustomControl1.Designer.vb。  
  
5.  如果使用的 C#，则在“代码编辑器”中打开CustomControl1.cs。  
  
6.  找到的类声明，该类继承自<xref:System.Windows.Forms.Control>。  
  
7.  将基类更改为要从中继承的控件。  
  
     例如，如果你想要从继承<xref:System.Windows.Forms.Button>，将类声明更改为以下：  
  
    ```vb  
    Partial Class CustomControl1  
        Inherits System.Windows.Forms.Button  
    ```  
  
    ```csharp  
    public partial class CustomControl1 : System.Windows.Forms.Button  
    ```  
  
8.  如果使用的是 Visual Basic，则保存并关闭 CustomControl1.Designer.vb。 在“代码编辑器”中打开 CustomControl1.vb。  
  
9. 实现控件将纳入的任何自定义方法或属性。  
  
10. 如果你想要修改您的控件的图形外观，重写<xref:System.Windows.Forms.Control.OnPaint%2A>方法。  
  
    > [!NOTE]
    >  重写<xref:System.Windows.Forms.Control.OnPaint%2A>将不允许您修改所有控件的外观。 所有由 Windows 完成其绘制这些控件 (例如， <xref:System.Windows.Forms.TextBox>) 永远不会调用其<xref:System.Windows.Forms.Control.OnPaint%2A>方法，因此将永远不会使用自定义代码。 你想要修改以查看是否特定控件的帮助文档，请参阅<xref:System.Windows.Forms.Control.OnPaint%2A>方法不可用。 有关所有 Windows 窗体控件的列表，请参阅[在 Windows 窗体上使用的控件](controls-to-use-on-windows-forms.md)。 如果控件不具有<xref:System.Windows.Forms.Control.OnPaint%2A>列为成员方法，您不能通过重写此方法更改其外观。 有关自定义绘制的详细信息，请参阅[自定义控件的绘制和呈现](custom-control-painting-and-rendering.md)。  
  
    ```vb  
    Protected Overrides Sub OnPaint(ByVal e As _  
       System.Windows.Forms.PaintEventArgs)  
       MyBase.OnPaint(e)  
       ' Insert code to do custom painting.   
       ' If you want to completely change the appearance of your control,  
       ' do not call MyBase.OnPaint(e).  
    End Sub  
    ```  
  
    ```csharp  
    protected override void OnPaint(PaintEventArgs pe)  
    {  
       base.OnPaint(pe);  
       // Insert code to do custom painting.  
       // If you want to completely change the appearance of your control,  
       // do not call base.OnPaint(pe).  
    }  
    ```  
  
11. 保存并测试控件。  
  
## <a name="see-also"></a>请参阅
- [各种自定义控件](varieties-of-custom-controls.md)
- [如何：从 Control 类继承](how-to-inherit-from-the-control-class.md)
- [如何：从 UserControl 类继承](how-to-inherit-from-the-usercontrol-class.md)
- [如何：Windows 窗体的作者控件](how-to-author-controls-for-windows-forms.md)
- [Visual Basic 中继承的事件处理程序疑难解答](~/docs/visual-basic/programming-guide/language-features/events/troubleshooting-inherited-event-handlers.md)
- [演练：从使用 Visual Basic 的 Windows 窗体控件继承](walkthrough-inheriting-from-a-windows-forms-control-with-visual-basic.md)
- [演练：从视觉对象的 Windows 窗体控件继承C#](walkthrough-inheriting-from-a-windows-forms-control-with-visual-csharp.md)
