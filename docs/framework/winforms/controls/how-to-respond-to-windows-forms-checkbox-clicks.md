---
title: 如何：响应 Windows 窗体 CheckBox 控件单击
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Click event [Windows Forms], CheckBox control
- CheckBox control [Windows Forms], Click events
- events [Windows Forms], Click events
- double-clicks
- check boxes [Windows Forms], responding to events
ms.assetid: c39f901e-8899-43b6-aa31-939cbf7089fb
ms.openlocfilehash: fff08bebf4e0eeea7dff8146ed8805e9d71247da
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57724496"
---
# <a name="how-to-respond-to-windows-forms-checkbox-clicks"></a>如何：响应 Windows 窗体 CheckBox 控件单击
每当用户单击 Windows 窗体<xref:System.Windows.Forms.CheckBox>控件，<xref:System.Windows.Forms.Control.Click>事件发生。 您可以在应用程序中执行某些操作根据复选框的状态。  
  
### <a name="to-respond-to-checkbox-clicks"></a>若要响应的复选框单击  
  
1.  在中<xref:System.Windows.Forms.Control.Click>事件处理程序，使用<xref:System.Windows.Forms.CheckBox.Checked%2A>属性来确定控件的状态，然后执行任何必要的操作。  
  
    ```vb  
    Private Sub CheckBox1_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles CheckBox1.Click  
       ' The CheckBox control's Text property is changed each time the   
       ' control is clicked, indicating a checked or unchecked state.  
       If CheckBox1.Checked = True Then  
          CheckBox1.Text = "Checked"  
       Else  
          CheckBox1.Text = "Unchecked"  
       End If  
    End Sub  
    ```  
  
    ```csharp  
    private void checkBox1_Click(object sender, System.EventArgs e)  
    {  
       // The CheckBox control's Text property is changed each time the   
       // control is clicked, indicating a checked or unchecked state.  
       if (checkBox1.Checked)  
       {  
          checkBox1.Text = "Checked";  
       }  
       else  
       {  
          checkBox1.Text = "Unchecked";  
       }  
    }  
    ```  
  
    ```cpp  
    private:  
       void checkBox1_CheckedChanged(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          if (checkBox1->Checked)  
          {  
             checkBox1->Text = "Checked";  
          }  
          else  
          {  
             checkBox1->Text = "Unchecked";  
          }  
       }  
    ```  
  
    > [!NOTE]
    >  如果用户尝试双击<xref:System.Windows.Forms.CheckBox>控件中，每次单击将单独处理; 即，<xref:System.Windows.Forms.CheckBox>控件不支持双击事件。  
  
    > [!NOTE]
    >  当<xref:System.Windows.Forms.CheckBox.AutoCheck%2A>属性是`true`（默认值），<xref:System.Windows.Forms.CheckBox>自动选中或清除时单击它。 否则，必须手动设置<xref:System.Windows.Forms.CheckBox.Checked%2A>属性时<xref:System.Windows.Forms.Control.Click>事件发生。  
  
     此外可以使用<xref:System.Windows.Forms.CheckBox>控件以确定操作过程。  
  
### <a name="to-determine-a-course-of-action-when-a-check-box-is-clicked"></a>若要确定一系列操作复选框时单击  
  
1.  使用 case 语句来查询的值<xref:System.Windows.Forms.CheckBox.CheckState%2A>属性来确定一系列操作。 当<xref:System.Windows.Forms.CheckBox.ThreeState%2A>属性设置为`true`，则<xref:System.Windows.Forms.CheckBox.CheckState%2A>属性可能返回三个可能的值，表示复选框已选中，框未选中或第三个不确定状态将显示的框与为灰色外观以表示该选项将不可用。  
  
    ```vb  
    Private Sub CheckBox1_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles CheckBox1.Click  
       Select Case CheckBox1.CheckState  
          Case CheckState.Checked  
             ' Code for checked state.  
          Case CheckState.Unchecked  
             ' Code for unchecked state.  
          Case CheckState.Indeterminate  
             ' Code for indeterminate state.  
       End Select   
    End Sub  
    ```  
  
    ```csharp  
    private void checkBox1_Click(object sender, System.EventArgs e)  
    {  
       switch(checkBox1.CheckState)  
       {  
          case CheckState.Checked:  
             // Code for checked state.  
             break;  
          case CheckState.Unchecked:  
             // Code for unchecked state.  
             break;  
          case CheckState.Indeterminate:  
             // Code for indeterminate state.  
             break;  
       }  
    }  
    ```  
  
    ```cpp  
    private:  
       void checkBox1_CheckedChanged(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          switch(checkBox1->CheckState) {  
             case CheckState::Checked:  
                // Code for checked state.  
                break;  
             case CheckState::Unchecked:  
                // Code for unchecked state.  
                break;  
             case CheckState::Indeterminate:  
                // Code for indeterminate state.  
                break;  
          }  
       }  
    ```  
  
    > [!NOTE]
    >  当<xref:System.Windows.Forms.CheckBox.ThreeState%2A>属性设置为`true`，则<xref:System.Windows.Forms.CheckBox.Checked%2A>属性将返回`true`同时<xref:System.Windows.Forms.CheckState.Checked>和<xref:System.Windows.Forms.CheckState.Indeterminate>。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.CheckBox>
- [CheckBox 控件概述](checkbox-control-overview-windows-forms.md)
- [如何：使用 Windows 窗体 CheckBox 控件设置选项](how-to-set-options-with-windows-forms-checkbox-controls.md)
- [CheckBox 控件](checkbox-control-windows-forms.md)
