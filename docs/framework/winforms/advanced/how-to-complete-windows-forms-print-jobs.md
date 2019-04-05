---
title: 如何：完整的 Windows 窗体打印作业
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- print jobs [Windows Forms], completing in Windows Forms
- printing [Windows Forms], print jobs
ms.assetid: 23ec74f7-34c5-4710-82a0-ee2914518548
ms.openlocfilehash: 1ae20e4fdc3a4fc3de8c462c355bcc700eddf22e
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57711728"
---
# <a name="how-to-complete-windows-forms-print-jobs"></a>如何：完整的 Windows 窗体打印作业
通常情况下，文字处理器和其他应用程序涉及打印将提供给打印作业已完成的用户显示一条消息的选项。 可以在 Windows 窗体中提供此功能，通过处理<xref:System.Drawing.Printing.PrintDocument.EndPrint>事件的<xref:System.Drawing.Printing.PrintDocument>组件。  
  
 下面的过程需要创建具有的基于 Windows 的应用程序<xref:System.Drawing.Printing.PrintDocument>组件，它将是启用从基于 Windows 的应用程序打印的标准方法。 有关从使用 Windows 窗体打印的详细信息<xref:System.Drawing.Printing.PrintDocument>组件，请参阅[如何：创建标准 Windows 窗体打印作业](how-to-create-standard-windows-forms-print-jobs.md)。  
  
### <a name="to-complete-a-print-job"></a>若要完成打印作业  
  
1.  设置<xref:System.Drawing.Printing.PrintDocument.DocumentName%2A>属性的<xref:System.Drawing.Printing.PrintDocument>组件。  
  
    ```vb  
    PrintDocument1.DocumentName = "MyTextFile"  
    ```  
  
    ```csharp  
    printDocument1.DocumentName = "MyTextFile";  
    ```  
  
    ```cpp  
    printDocument1->DocumentName = "MyTextFile";  
    ```  
  
2.  编写代码以处理 <xref:System.Drawing.Printing.PrintDocument.EndPrint> 事件。  
  
     在下面的代码示例中，将显示一个消息框，并指示文档已完成打印。  
  
    ```vb  
    Private Sub PrintDocument1_EndPrint(ByVal sender As Object, ByVal e As System.Drawing.Printing.PrintEventArgs) Handles PrintDocument1.EndPrint  
       MessageBox.Show(PrintDocument1.DocumentName + " has finished printing.")  
    End Sub  
    ```  
  
    ```csharp  
    private void printDocument1_EndPrint(object sender,   
    System.Drawing.Printing.PrintEventArgs e)  
    {  
       MessageBox.Show(printDocument1.DocumentName +   
          " has finished printing.");  
    }  
    ```  
  
    ```cpp  
    private:  
       void printDocument1_EndPrint(System::Object ^ sender,  
          System::Drawing::Printing::PrintEventArgs ^ e)  
       {  
          MessageBox::Show(String::Concat(printDocument1->DocumentName,  
             " has finished printing."));  
       }  
    ```  
  
     (Visual C# 和[!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]) 将以下代码放在窗体的构造函数，以注册事件处理程序。  
  
    ```csharp  
    this.printDocument1.EndPrint += new  
       System.Drawing.Printing.PrintEventHandler  
       (this.printDocument1_EndPrint);  
    ```  
  
    ```cpp  
    this->printDocument1->EndPrint += gcnew  
       System::Drawing::Printing::PrintEventHandler  
       (this, &Form1::printDocument1_EndPrint);  
    ```  
  
## <a name="see-also"></a>请参阅
- <xref:System.Drawing.Printing.PrintDocument>
- [Windows 窗体打印支持](windows-forms-print-support.md)
