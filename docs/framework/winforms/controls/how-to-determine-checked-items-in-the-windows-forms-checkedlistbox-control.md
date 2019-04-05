---
title: 如何：确定 Windows 窗体 CheckedListBox 控件中的选中的项
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- check boxes [Windows Forms], determining checked state
- CheckedListBox control [Windows Forms], determining checked state
ms.assetid: 178b477d-27c9-489c-8914-44a9623a4d41
ms.openlocfilehash: 2936a64338f47107b11b5f6eb85c5e94707bf926
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57707958"
---
# <a name="how-to-determine-checked-items-in-the-windows-forms-checkedlistbox-control"></a>如何：确定 Windows 窗体 CheckedListBox 控件中的选中的项
在 Windows 窗体中显示数据时<xref:System.Windows.Forms.CheckedListBox>控件，您可以或者循环访问集合中存储<xref:System.Windows.Forms.CheckedListBox.CheckedItems%2A>属性或逐步执行列表使用<xref:System.Windows.Forms.CheckedListBox.GetItemChecked%2A>方法，以确定未选中的项。 <xref:System.Windows.Forms.CheckedListBox.GetItemChecked%2A>方法将项索引号作为其参数并返回`true`或`false`。 与您所料，相反<xref:System.Windows.Forms.ListBox.SelectedItems%2A>和<xref:System.Windows.Forms.ListBox.SelectedIndices%2A>属性不用于确定未选中的项; 它们确定哪些项会突出显示。  
  
### <a name="to-determine-checked-items-in-a-checkedlistbox-control"></a>若要确定 CheckedListBox 控件中的选中的项  
  
1.  循环访问<xref:System.Windows.Forms.CheckedListBox.CheckedItems%2A>0 开始，因为集合是从零开始的集合。 请注意，此方法将向您提供的项编号的列表中选中的项，不是整个列表。 因此，如果未选中列表中的第一个项并选中第二个项，下面的代码将显示类似文本"选中的项 1 = MyListItem2"。  
  
    ```vb  
    ' Determine if there are any items checked.  
    If CheckedListBox1.CheckedItems.Count <> 0 Then  
       ' If so, loop through all checked items and print results.  
       Dim x As Integer  
       Dim s As String = ""  
       For x = 0 To CheckedListBox1.CheckedItems.Count - 1  
          s = s & "Checked Item " & (x + 1).ToString & " = " & CheckedListBox1.CheckedItems(x).ToString & ControlChars.CrLf  
       Next x  
       MessageBox.Show(s)  
    End If  
    ```  
  
    ```csharp  
    // Determine if there are any items checked.  
    if(checkedListBox1.CheckedItems.Count != 0)  
    {  
       // If so, loop through all checked items and print results.  
       string s = "";  
       for(int x = 0; x < checkedListBox1.CheckedItems.Count ; x++)  
       {  
          s = s + "Checked Item " + (x+1).ToString() + " = " + checkedListBox1.CheckedItems[x].ToString() + "\n";  
       }  
       MessageBox.Show(s);  
    }  
    ```  
  
    ```cpp  
    // Determine if there are any items checked.  
    if(checkedListBox1->CheckedItems->Count != 0)  
    {  
       // If so, loop through all checked items and print results.  
       String ^ s = "";  
       for(int x = 0; x < checkedListBox1->CheckedItems->Count; x++)  
       {  
          s = String::Concat(s, "Checked Item ", (x+1).ToString(),  
             " = ", checkedListBox1->CheckedItems[x]->ToString(),  
             "\n");  
       }  
       MessageBox::Show(s);  
    }  
    ```  
  
     - 或 -  
  
2.  单步执行<xref:System.Windows.Forms.CheckedListBox.Items%2A>集合，从 0 开始因为集合是从零开始，并调用<xref:System.Windows.Forms.CheckedListBox.GetItemChecked%2A>方法的每个项。 请注意，此方法将向您提供的项编号在总体的列表中，因此如果第一项不会检查列表并选中第二个项，它将显示类似于"项 2 = MyListItem2"。  
  
    ```vb  
    Dim i As Integer  
    Dim s As String  
    s = "Checked Items:" & ControlChars.CrLf  
    For i = 0 To (CheckedListBox1.Items.Count - 1)  
       If CheckedListBox1.GetItemChecked(i) = True Then  
          s = s & "Item " & (i + 1).ToString & " = " & CheckedListBox1.Items(i).ToString & ControlChars.CrLf  
       End If  
    Next  
    MessageBox.Show(s)  
    ```  
  
    ```csharp  
    int i;  
    string s;   
    s = "Checked items:\n" ;  
    for (i = 0; i <= (checkedListBox1.Items.Count-1); i++)  
    {  
       if (checkedListBox1.GetItemChecked(i))  
       {  
          s = s + "Item " + (i+1).ToString() + " = " + checkedListBox1.Items[i].ToString() + "\n";  
       }  
    }  
    MessageBox.Show (s);  
    ```  
  
    ```cpp  
    int i;  
    String ^ s;   
    s = "Checked items:\n" ;  
    for (i = 0; i <= (checkedListBox1->Items->Count-1); i++)  
    {  
       if (checkedListBox1->GetItemChecked(i))  
       {  
          s = String::Concat(s, "Item ", (i+1).ToString(), " = ",  
             checkedListBox1->Item[i]->ToString(), "\n");  
       }  
    }  
    MessageBox::Show(s);  
    ```  
  
## <a name="see-also"></a>请参阅
- [用于列出选项的 Windows 窗体控件](windows-forms-controls-used-to-list-options.md)
