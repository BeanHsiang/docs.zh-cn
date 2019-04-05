---
title: 如何：将 Windows 窗体 ComboBox 或 ListBox 控件绑定到数据
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data [Windows Forms], binding to controls
- list boxes [Windows Forms], data binding
- ComboBox control [Windows Forms], data binding
- data binding [Windows Forms], combo boxes
- ListBox control [Windows Forms], data binding
- combo boxes [Windows Forms], data binding
- bound controls [Windows Forms], combo boxes
- Windows Forms controls, data binding
- data-bound controls [Windows Forms], Windows Forms
ms.assetid: dfd7f081-8bea-4a41-86a3-86a1934828ef
ms.openlocfilehash: c8eb224cbb8ec7ab271edaed8bb25f9cc7fb8ddc
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57709921"
---
# <a name="how-to-bind-a-windows-forms-combobox-or-listbox-control-to-data"></a>如何：将 Windows 窗体 ComboBox 或 ListBox 控件绑定到数据
可以将绑定<xref:System.Windows.Forms.ComboBox>和<xref:System.Windows.Forms.ListBox>到数据以执行任务，例如浏览数据库中的数据，输入新数据，或编辑现有数据。  
  
### <a name="to-bind-a-combobox-or-listbox-control"></a>若要将 ComboBox 或 ListBox 控件绑定  
  
1.  设置`DataSource`到数据源对象的属性。 可能的数据源包括<xref:System.Windows.Forms.BindingSource>绑定到数据、 数据表、 数据视图、 数据集，数据视图，管理器、 一个数组或实现任何类<xref:System.Collections.IList>接口。 有关详细信息，请参阅[支持的 Windows 窗体数据源](../data-sources-supported-by-windows-forms.md)。  
  
2.  如果要绑定到一个表，设置`DisplayMember`属性设置为数据源中的列的名称。  
  
     \- 或 -  
  
     如果要绑定到<xref:System.Collections.IList>，将显示成员设置为列表中的类型的公共属性。  
  
    ```vb  
    Private Sub BindComboBox()  
      ComboBox1.DataSource = DataSet1.Tables("Suppliers")  
      ComboBox1.DisplayMember = "ProductName"  
    End Sub  
    ```  
  
    ```csharp  
    private void BindComboBox()  
    {  
      comboBox1.DataSource = dataSet1.Tables["Suppliers"];  
      comboBox1.DisplayMember = "ProductName";  
    }  
    ```  
  
    > [!NOTE]
    >  如果绑定到数据源不实现<xref:System.ComponentModel.IBindingList>接口，如<xref:System.Collections.ArrayList>，更新数据源时，将不会更新绑定的控件的数据。 例如，如果您有一个组合框绑定到<xref:System.Collections.ArrayList>并将数据添加到<xref:System.Collections.ArrayList>，这些新项将不会显示在组合框中。 但是，可以强制组合框，以通过调用更新<xref:System.Windows.Forms.BindingManagerBase.SuspendBinding%2A>并<xref:System.Windows.Forms.BindingManagerBase.ResumeBinding%2A>的实例上的方法<xref:System.Windows.Forms.BindingContext>控件所绑定到类。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.ComboBox>
- <xref:System.Windows.Forms.ListBox>
- [Windows 窗体数据绑定](../windows-forms-data-binding.md)
- [数据绑定和 Windows 窗体](../data-binding-and-windows-forms.md)
- [用于列出选项的 Windows 窗体控件](windows-forms-controls-used-to-list-options.md)
