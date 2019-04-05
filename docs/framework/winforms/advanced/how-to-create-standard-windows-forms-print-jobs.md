---
title: 如何：创建标准 Windows 窗体打印作业
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- printing [Windows Forms]
- printing [Windows Forms], creating print jobs
- printing [Visual Basic], in Windows applications
ms.assetid: 03342b90-9cfe-40b2-838b-b479a13c5dea
ms.openlocfilehash: b0568472dadceb46257a8d35211034a718aef74c
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57705215"
---
# <a name="how-to-create-standard-windows-forms-print-jobs"></a>如何：创建标准 Windows 窗体打印作业
在 Windows 窗体中打印的基础是<xref:System.Drawing.Printing.PrintDocument>组件 — 具体而言，<xref:System.Drawing.Printing.PrintDocument.PrintPage>事件。 通过编写代码来处理<xref:System.Drawing.Printing.PrintDocument.PrintPage>事件，可以指定打印内容以及如何打印它。  
  
### <a name="to-create-a-print-job"></a>若要创建打印作业  
  
1.  添加<xref:System.Drawing.Printing.PrintDocument>向窗体组件。  
  
2.  编写代码以处理 <xref:System.Drawing.Printing.PrintDocument.PrintPage> 事件。  
  
     必须编写打印逻辑的代码。 此外，必须指定要打印的材料。  
  
     在下面的代码示例中创建一个红色矩形形状中的示例图形<xref:System.Drawing.Printing.PrintDocument.PrintPage>事件处理程序，使其作为要打印的材料。  
  
    ```vb  
    Private Sub PrintDocument1_PrintPage(ByVal sender As Object, ByVal e As System.Drawing.Printing.PrintPageEventArgs) Handles PrintDocument1.PrintPage  
       e.Graphics.FillRectangle(Brushes.Red, New Rectangle(500, 500, 500, 500))  
    End Sub  
    ```  
  
    ```csharp  
    private void printDocument1_PrintPage(object sender,   
    System.Drawing.Printing.PrintPageEventArgs e)  
    {  
       e.Graphics.FillRectangle(Brushes.Red,   
         new Rectangle(500, 500, 500, 500));  
    }  
    ```  
  
    ```cpp  
    private:  
       void printDocument1_PrintPage(System::Object ^ sender,  
          System::Drawing::Printing::PrintPageEventArgs ^ e)  
       {  
          e->Graphics->FillRectangle(Brushes::Red,  
             Rectangle(500, 500, 500, 500));  
       }  
    ```  
  
     (Visual C# 和[!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]) 将以下代码放在窗体的构造函数，以注册事件处理程序。  
  
    ```csharp  
    this.printDocument1.PrintPage += new  
       System.Drawing.Printing.PrintPageEventHandler  
       (this.printDocument1_PrintPage);  
    ```  
  
    ```cpp  
    printDocument1->PrintPage += gcnew  
       System::Drawing::Printing::PrintPageEventHandler  
       (this, &Form1::printDocument1_PrintPage);  
    ```  
  
     您可能还想要编写代码<xref:System.Drawing.Printing.PrintDocument.BeginPrint>和<xref:System.Drawing.Printing.PrintDocument.EndPrint>事件，可能包括一个整数表示总页数进行打印，即每一页打印会相应减少。  
  
    > [!NOTE]
    >  您可以添加<xref:System.Windows.Forms.PrintDialog>向窗体以向用户提供干净且高效的用户界面 (UI) 组件。 设置<xref:System.Windows.Forms.PrintDialog.Document%2A>属性的<xref:System.Windows.Forms.PrintDialog>组件允许您设置与打印相关的属性记录你正在使用窗体上。 有关详细信息<xref:System.Windows.Forms.PrintDialog>组件，请参阅[PrintDialog 组件](../controls/printdialog-component-windows-forms.md)。  
  
     有关详细信息的 Windows 窗体的详细信息包括如何以编程方式创建打印作业的打印作业，请参阅<xref:System.Drawing.Printing.PrintPageEventArgs>。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Drawing.Printing.PrintDocument>
- [Windows 窗体打印支持](windows-forms-print-support.md)
