---
title: 如何：显示打印预览在 Windows 窗体应用程序
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- print preview [Windows Forms], displaying
- printing [Windows Forms], print preview
- examples [Windows Forms], print preview
ms.assetid: e394134c-0886-4517-bd8d-edc4a3749eb5
ms.openlocfilehash: 13510086edb13ff54f5551296c1b64c51873f649
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57715355"
---
# <a name="how-to-display-print-preview-in-windows-forms-applications"></a>如何：显示打印预览在 Windows 窗体应用程序
可以使用<xref:System.Windows.Forms.PrintPreviewDialog>以使用户能够显示文档时，通常前要打印的控制。  
  
 若要执行此操作，需要指定的实例<xref:System.Drawing.Printing.PrintDocument>类; 这是要打印的文档。 有关使用打印预览的详细信息<xref:System.Drawing.Printing.PrintDocument>组件，请参阅[如何：使用打印预览的 Windows 窗体中打印](../advanced/how-to-print-in-windows-forms-using-print-preview.md)。  
  
> [!NOTE]
>  若要使用<xref:System.Windows.Forms.PrintPreviewDialog>控件在运行时，用户必须已经安装了打印机其计算机上本地或通过网络，因为这会影响如何<xref:System.Windows.Forms.PrintPreviewDialog>组件确定文档的打印效果。  
  
 <xref:System.Windows.Forms.PrintPreviewDialog>控件使用<xref:System.Drawing.Printing.PrinterSettings>类。 此外，<xref:System.Windows.Forms.PrintPreviewDialog>控件使用<xref:System.Drawing.Printing.PageSettings>类，就像<xref:System.Windows.Forms.PrintPreviewDialog>组件相同。 中指定的打印文档<xref:System.Windows.Forms.PrintPreviewDialog>控件的<xref:System.Windows.Forms.PrintPreviewControl.Document%2A>属性是指两个实例<xref:System.Drawing.Printing.PrinterSettings>和<xref:System.Drawing.Printing.PageSettings>类，并将这些用于呈现预览窗口中的文档。  
  
### <a name="to-view-pages-using-the-printpreviewdialog-control"></a>若要查看使用 PrintPreviewDialog 控件的网页  
  
-   使用 <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> 方法可显示对话框，从而指定要使用的 <xref:System.Drawing.Printing.PrintDocument> 。  
  
     在下面的代码示例中，<xref:System.Windows.Forms.Button>控件的<xref:System.Windows.Forms.Control.Click>事件处理程序打开的实例<xref:System.Windows.Forms.PrintPreviewDialog>控件。 中指定打印文档<xref:System.Windows.Forms.PrintDialog.Document%2A>属性。 在下面的示例中，未不指定任何打印文档。  
  
     该示例需要窗体具有<xref:System.Windows.Forms.Button>控件，<xref:System.Drawing.Printing.PrintDocument>名为组件`myDocument`，和一个<xref:System.Windows.Forms.PrintPreviewDialog>控件。  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, _  
       ByVal e As System.EventArgs) Handles Button1.Click  
       ' The print document 'myDocument' used below  
       ' is merely for an example.  
       ' You will have to specify your own print document.  
       PrintPreviewDialog1.Document = myDocument  
       PrintPreviewDialog1.ShowDialog()  
    End Sub  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       // The print document 'myDocument' used below  
       // is merely for an example.  
       // You will have to specify your own print document.  
       printPreviewDialog1.Document = myDocument;  
       printPreviewDialog1.ShowDialog();  
    }  
    ```  
  
    ```cpp  
    private:  
       void button1_Click(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          // The print document 'myDocument' used below  
          // is merely for an example.  
          // You will have to specify your own print document.  
          printPreviewDialog1->Document = myDocument;  
          printPreviewDialog1->ShowDialog();  
       }  
    ```  
  
     (Visual C#， [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]) 将以下代码放在窗体的构造函数，以注册事件处理程序。  
  
    ```csharp  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
    ```  
  
    ```cpp  
    this->button1->Click += gcnew  
       System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
## <a name="see-also"></a>请参阅
- [PrintDocument 组件](printdocument-component-windows-forms.md)
- [PrintPreviewDialog 控件](printpreviewdialog-control-windows-forms.md)
- [Windows 窗体打印支持](../advanced/windows-forms-print-support.md)
- [Windows 窗体](../index.md)
