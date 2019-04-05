---
title: 如何：对于表格验证使用 Windows 窗体 ErrorProvider 组件显示错误图标
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- errors [Windows Forms], displaying to users
- error icons
- ErrorProvider component [Windows Forms], displaying error icons
- error messages [Windows Forms], displaying icons
ms.assetid: 3b681a32-9db4-497b-a34b-34980eabee46
ms.openlocfilehash: f676454849c37da8c0a5f944be05c3f6c95887b4
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57707633"
---
# <a name="how-to-display-error-icons-for-form-validation-with-the-windows-forms-errorprovider-component"></a>如何：对于表格验证使用 Windows 窗体 ErrorProvider 组件显示错误图标
可以使用 Windows 窗体<xref:System.Windows.Forms.ErrorProvider>组件，用户输入无效数据时显示错误图标。 您必须具有至少两个选项卡上，它们之间并由此调用验证代码以窗体控件。  
  
### <a name="to-display-an-error-icon-when-a-controls-value-is-invalid"></a>若要在控件的值无效时显示错误图标  
  
1.  添加两个控件 — 例如，文本框中，向 Windows 窗体。  
  
2.  添加<xref:System.Windows.Forms.ErrorProvider>组件到窗体。  
  
3.  选择第一个控件，然后将代码添加到其<xref:System.Windows.Forms.Control.Validating>事件处理程序。 为了使此代码正常运行，该过程必须连接到该事件。 有关详细信息，请参阅[如何：在运行时为 Windows 窗体创建事件处理程序](../how-to-create-event-handlers-at-run-time-for-windows-forms.md)。  
  
     下面的代码测试用户输入; 这些数据的有效性如果数据是无效的<xref:System.Windows.Forms.ErrorProvider.SetError%2A>调用方法。 第一个参数<xref:System.Windows.Forms.ErrorProvider.SetError%2A>方法指定用于控制为旁边显示图标。 第二个参数是要显示的错误文本。  
  
    ```vb  
    Private Sub TextBox1_Validating(ByVal Sender As Object, _  
       ByVal e As System.ComponentModel.CancelEventArgs) Handles _  
       TextBox1.Validating  
          If Not IsNumeric(TextBox1.Text) Then  
             ErrorProvider1.SetError(TextBox1, "Not a numeric value.")  
          Else  
             ' Clear the error.  
             ErrorProvider1.SetError(TextBox1, "")  
          End If  
    End Sub  
    ```  
  
    ```csharp  
    protected void textBox1_Validating (object sender,  
       System.ComponentModel.CancelEventArgs e)  
    {  
       try  
       {  
          int x = Int32.Parse(textBox1.Text);  
          errorProvider1.SetError(textBox1, "");  
       }  
       catch (Exception ex)  
       {  
          errorProvider1.SetError(textBox1, "Not an integer value.");  
       }  
    }  
    ```  
  
    ```cpp  
    private:  
       System::Void textBox1_Validating(System::Object ^  sender,  
          System::ComponentModel::CancelEventArgs ^  e)  
       {  
          try  
          {  
             int x = Int32::Parse(textBox1->Text);  
             errorProvider1->SetError(textBox1, "");  
          }  
          catch (System::Exception ^ ex)  
          {  
             errorProvider1->SetError(textBox1, "Not an integer value.");  
          }  
       }  
    ```  
  
     (Visual C#， [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]) 将以下代码放在窗体的构造函数，以注册事件处理程序。  
  
    ```csharp  
    this.textBox1.Validating += new  
    System.ComponentModel.CancelEventHandler(this.textBox1_Validating);  
    ```  
  
    ```cpp  
    this->textBox1->Validating += gcnew  
       System::ComponentModel::CancelEventHandler  
       (this, &Form1::textBox1_Validating);  
    ```  
  
4.  运行该项目。 在第一个控件，然后第二个选项卡中键入无效 （在此示例中，非数字） 的数据。 当显示错误图标时，指向它使用鼠标指针以查看错误文本。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.ErrorProvider.SetError%2A>
- [ErrorProvider 组件概述](errorprovider-component-overview-windows-forms.md)
- [如何：在一个数据集中使用 Windows 窗体 ErrorProvider 组件查看错误](view-errors-within-a-dataset-with-wf-errorprovider-component.md)
