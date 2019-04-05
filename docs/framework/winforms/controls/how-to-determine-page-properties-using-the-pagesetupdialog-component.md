---
title: 如何：使用 PageSetupDialog 组件确定页属性
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- page properties
- page setup
- PageSetupDialog component
ms.assetid: 6dae05bc-c0fd-4357-bb93-841a1631d98f
ms.openlocfilehash: 482825c1e17811b31c3520a0280d7d0434489bf5
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57713197"
---
# <a name="how-to-determine-page-properties-using-the-pagesetupdialog-component"></a>如何：使用 PageSetupDialog 组件确定页属性
[PageSetupDialog](pagesetupdialog-component-windows-forms.md) 组件针对文档向用户呈现布局、纸张大小和其他页面布局选项。  
  
 需要指定 <xref:System.Drawing.Printing.PrintDocument> 类的实例 — 这是要打印的文档。 此外，用户必须在其计算机上安装打印机（本地或通过网络），因为 <xref:System.Windows.Forms.PageSetupDialog> 组件在一定程度上会通过此方面确定向用户呈现的页面格式设置选项。  
  
 使用 <xref:System.Windows.Forms.PageSetupDialog> 组件的一个重要方面是它如何与 <xref:System.Drawing.Printing.PageSettings> 类进行交互。 <xref:System.Drawing.Printing.PageSettings> 类用于指定修改页面打印方式的设置，如纸张方向、页面大小和边距。 这些设置中的每个设置都表示为 <xref:System.Drawing.Printing.PageSettings> 类的属性。 <xref:System.Windows.Forms.PageSetupDialog> 类会为与文档关联（并表示为 <xref:System.Drawing.Printing.PageSettings> 属性）的给定 <xref:System.Drawing.Printing.PrintDocument.DefaultPageSettings%2A> 类实例修改这些属性值。  
  
### <a name="to-set-page-properties-using-the-pagesetupdialog-component"></a>使用 PageSetupDialog 组件设置页面属性  
  
1.  使用 <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> 方法可显示对话框，从而指定要使用的 <xref:System.Drawing.Printing.PrintDocument> 。  
  
     在以下示例中， <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.Click> 事件处理程序会打开 <xref:System.Windows.Forms.PageSetupDialog> 组件的实例。 一个现有文档在 <xref:System.Windows.Forms.PageSetupDialog.Document%2A> 属性中进行指定，其 <xref:System.Drawing.Printing.PageSettings.Color%2A?displayProperty=nameWithType> 属性设置为 `false`。  
  
     该示例假定窗体具有<xref:System.Windows.Forms.Button>控件，<xref:System.Drawing.Printing.PrintDocument>名为组件`myDocument`，和一个<xref:System.Windows.Forms.PageSetupDialog>组件。  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, _  
    ByVal e As System.EventArgs) Handles Button1.Click  
       ' The print document 'myDocument' used below  
       ' is merely for an example.  
       'You will have to specify your own print document.  
       PageSetupDialog1.Document = myDocument  
       ' Sets the print document's color setting to false,  
       ' so that the page will not be printed in color.  
       PageSetupDialog1.Document.DefaultPageSettings.Color = False  
       PageSetupDialog1.ShowDialog()  
    End Sub  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       // The print document 'myDocument' used below  
       // is merely for an example.  
       // You will have to specify your own print document.  
       pageSetupDialog1.Document = myDocument;  
       // Sets the print document's color setting to false,  
       // so that the page will not be printed in color.  
       pageSetupDialog1.Document.DefaultPageSettings.Color = false;  
       pageSetupDialog1.ShowDialog();  
    }  
    ```  
  
    ```cpp  
    private:  
       System::Void button1_Click(System::Object ^  sender,  
          System::EventArgs ^  e)  
       {  
          // The print document 'myDocument' used below  
          // is merely for an example.  
          // You will have to specify your own print document.  
          pageSetupDialog1->Document = myDocument;  
          // Sets the print document's color setting to false,  
          // so that the page will not be printed in color.  
          pageSetupDialog1->Document->DefaultPageSettings->Color = false;  
          pageSetupDialog1->ShowDialog();  
       }  
    ```  
  
     (Visual C# 和[!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]) 将以下代码放在窗体的构造函数，以注册事件处理程序。  
  
    ```csharp  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
    ```  
  
    ```cpp  
    this->button1->Click += gcnew   
       System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.PageSetupDialog>
- [如何：创建标准 Windows 窗体打印作业](../advanced/how-to-create-standard-windows-forms-print-jobs.md)
- [PageSetupDialog 组件](pagesetupdialog-component-windows-forms.md)
