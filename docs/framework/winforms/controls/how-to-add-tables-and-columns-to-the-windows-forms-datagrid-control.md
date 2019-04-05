---
title: 如何：向 Windows 窗体 DataGrid 控件添加表和列
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- columns [Windows Forms], adding to DataGrid control
- tables [Windows Forms], adding to DataGrid control
- DataGrid control [Windows Forms], adding tables and columns
ms.assetid: 2fe661b9-aa06-49b9-a314-a0d3cbfdcb4d
ms.openlocfilehash: e222227d6283555fa4ec25fe1e5d8e661296034f
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57709154"
---
# <a name="how-to-add-tables-and-columns-to-the-windows-forms-datagrid-control"></a>如何：向 Windows 窗体 DataGrid 控件添加表和列
> [!NOTE]
>  
  <xref:System.Windows.Forms.DataGridView> 控件取代了 <xref:System.Windows.Forms.DataGrid> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.DataGrid> 控件以实现向后兼容并供将来使用。 有关详细信息，请参阅 [Windows 窗体 DataGridView 控件与 DataGrid 控件之间的区别](differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)。  
  
 可以在 Windows 窗体中显示数据<xref:System.Windows.Forms.DataGrid>控件中的表和列创建**DataGridTableStyle**对象并将它们添加到**GridTableStylesCollection**对象，它是通过访问<xref:System.Windows.Forms.DataGrid>控件的**TableStyles**属性。 每个表样式显示任何数据的表中指定的内容**DataGridTableStyle**对象的**MappingName**属性。 默认情况下，具有未指定的列样式的表样式将显示该数据表中的所有列。 你可以限制在表中的哪些列显示通过添加**DataGridColumnStyle**对象添加到**GridColumnStylesCollection**对象，通过访问**GridColumnStyles**每个属性**DataGridTableStyle**对象。  
  
### <a name="to-add-a-table-and-column-to-a-datagrid-programmatically"></a>若要以编程方式将表和列添加到数据网格  
  
1.  若要在表中显示数据，您必须首先绑定<xref:System.Windows.Forms.DataGrid>控件向数据集。 有关详细信息，请参阅[如何：将 Windows 窗体 DataGrid 控件绑定到数据源](how-to-bind-the-windows-forms-datagrid-control-to-a-data-source.md)。  
  
    > [!CAUTION]
    >  以编程方式指定列样式，将始终创建**DataGridColumnStyle**对象，并将其添加到**GridColumnStylesCollection**对象然后再添加**DataGridTableStyle**对象添加到**GridTableStylesCollection**对象。 当添加一个空**DataGridTableStyle**对象添加到收藏**DataGridColumnStyle**为你自动生成的对象。 如果你尝试添加新因此，将引发异常**DataGridColumnStyle**对象具有重复**MappingName**值到**GridColumnStylesCollection**对象。  
  
2.  声明新的表样式，并将其映射名称设置。  
  
    ```vb  
    Dim ts1 As New DataGridTableStyle()  
    ts1.MappingName = "Customers"  
    ```  
  
    ```csharp  
    DataGridTableStyle ts1 = new DataGridTableStyle();  
    ts1.MappingName = "Customers";  
    ```  
  
    ```cpp  
    DataGridTableStyle* ts1 = new DataGridTableStyle();  
    ts1->MappingName = S"Customers";  
    ```  
  
3.  声明新的列样式并设置其映射名称和其他属性。  
  
    ```vb  
    Dim myDataCol As New DataGridBoolColumn()  
    myDataCol.HeaderText = "My New Column"  
    myDataCol.MappingName = "Current"  
    ```  
  
    ```csharp  
    DataGridBoolColumn myDataCol = new DataGridBoolColumn();  
    myDataCol.HeaderText = "My New Column";  
    myDataCol.MappingName = "Current";  
    ```  
  
    ```cpp  
    DataGridBoolColumn^ myDataCol = gcnew DataGridBoolColumn();  
    myDataCol->HeaderText = "My New Column";  
    myDataCol->MappingName = "Current";  
    ```  
  
4.  调用**外**方法**GridColumnStylesCollection**对象将列添加到表样式  
  
    ```vb  
    ts1.GridColumnStyles.Add(myDataCol)  
    ```  
  
    ```csharp  
    ts1.GridColumnStyles.Add(myDataCol);  
    ```  
  
    ```cpp  
    ts1->GridColumnStyles->Add(myDataCol);  
    ```  
  
5.  调用**外**方法**GridTableStylesCollection**要添加到数据网格的表样式对象。  
  
    ```vb  
    DataGrid1.TableStyles.Add(ts1)  
    ```  
  
    ```csharp  
    dataGrid1.TableStyles.Add(ts1);  
    ```  
  
    ```cpp  
    dataGrid1->TableStyles->Add(ts1);  
    ```  
  
## <a name="see-also"></a>请参阅
- [DataGrid 控件](datagrid-control-windows-forms.md)
- [如何：删除或隐藏 Windows 窗体 DataGrid 控件中的列](how-to-delete-or-hide-columns-in-the-windows-forms-datagrid-control.md)
