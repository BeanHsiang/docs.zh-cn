---
title: 如何：在 Windows 窗体中打印图形
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- graphics [Windows Forms], printing
- printing [Windows Forms], graphics
ms.assetid: 32b891e6-52ff-4fea-a9ff-2ce5db20a4c6
ms.openlocfilehash: cb8c9f291103915c82fb31af5c6668fbd0648f66
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57721299"
---
# <a name="how-to-print-graphics-in-windows-forms"></a>如何：在 Windows 窗体中打印图形
通常情况下，想要在基于 Windows 的应用程序中打印图形。 <xref:System.Drawing.Graphics>类提供了对象绘制到设备，如屏幕或打印机的方法。  
  
### <a name="to-print-graphics"></a>若要打印图形  
  
1.  添加<xref:System.Drawing.Printing.PrintDocument>向窗体组件。  
  
2.  在中<xref:System.Drawing.Printing.PrintDocument.PrintPage>事件处理程序，使用<xref:System.Drawing.Printing.PrintPageEventArgs.Graphics%2A>属性的<xref:System.Drawing.Printing.PrintPageEventArgs>类，以指示要打印的图形类型上的打印机。  
  
     下面的代码示例显示了用于创建一个蓝色的椭圆的边框内的事件处理程序。 矩形具有的以下位置和尺寸： 开始为 100，150 具有 250 的宽度和高度为 250。  
  
    ```vb  
    Private Sub PrintDocument1_PrintPage(ByVal sender As Object, ByVal e As System.Drawing.Printing.PrintPageEventArgs) Handles PrintDocument1.PrintPage  
       e.Graphics.FillEllipse(Brushes.Blue, New Rectangle(100, 150, 250, 250))  
    End Sub  
    ```  
  
    ```csharp  
    private void printDocument1_PrintPage(object sender,   
    System.Drawing.Printing.PrintPageEventArgs e)  
    {  
       e.Graphics.FillRectangle(Brushes.Blue,   
         new Rectangle(100, 150, 250, 250));  
    }  
    ```  
  
    ```cpp  
    private:  
       void printDocument1_PrintPage(System::Object ^ sender,  
          System::Drawing::Printing::PrintPageEventArgs ^ e)  
       {  
          e->Graphics->FillRectangle(Brushes::Blue,  
             Rectangle(100, 150, 250, 250));  
       }  
    ```  
  
     (Visual C# 和[!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]) 将以下代码放在窗体的构造函数，以注册事件处理程序。  
  
    ```csharp  
    this.printDocument1.PrintPage += new  
       System.Drawing.Printing.PrintPageEventHandler  
       (this.printDocument1_PrintPage);  
    ```  
  
    ```cpp  
    this->printDocument1->PrintPage += gcnew  
       System::Drawing::Printing::PrintPageEventHandler  
       (this, &Form1::printDocument1_PrintPage);  
    ```  
  
## <a name="see-also"></a>请参阅
- <xref:System.Drawing.Graphics>
- <xref:System.Drawing.Brush>
- [Windows 窗体打印支持](windows-forms-print-support.md)
