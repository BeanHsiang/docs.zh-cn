---
title: 如何：排序和筛选 ADO.NET 数据与 Windows 窗体 BindingSource 组件
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- sorting data
- data sorting [Windows Forms], ADO.NET
- data [Windows Forms], filtering
- BindingSource component [Windows Forms], sorting and filtering data
- filtering [Windows Forms], ADO.NET
- data [Windows Forms], sorting
- ADO.NET [Windows Forms]
ms.assetid: 6c206daf-d706-4602-9dbe-435343052063
ms.openlocfilehash: 65be2367091144945e9540c848e6131deac9d725
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57703096"
---
# <a name="how-to-sort-and-filter-adonet-data-with-the-windows-forms-bindingsource-component"></a>如何：排序和筛选 ADO.NET 数据与 Windows 窗体 BindingSource 组件
排序和筛选功能可以公开<xref:System.Windows.Forms.BindingSource>通过控制<xref:System.Windows.Forms.BindingSource.Sort%2A>和<xref:System.Windows.Forms.BindingSource.Filter%2A>属性。 您可以将简单排序的基础数据源，则应用<xref:System.ComponentModel.IBindingList>，并可以应用筛选和高级排序数据源时<xref:System.ComponentModel.IBindingListView>。 <xref:System.Windows.Forms.BindingSource.Sort%2A>属性需要标准[!INCLUDE[vstecado](../../../../includes/vstecado-md.md)]语法： 一个表示数据源中数据的列的名称的字符串后跟`ASC`或`DESC`以指示是按升序或降序顺序对列表进行排序。 您可以设置高级排序或通过使用逗号分隔符分隔每个列的多个列排序。 <xref:System.Windows.Forms.BindingSource.Filter%2A>属性采用的字符串表达式。  
  
> [!NOTE]
>  将敏感信息（如密码）存储在连接字符串中可能会影响应用程序的安全性。 若要控制对数据库的访问，一种较为安全的方法是使用 Windows 身份验证（也称为集成安全性）。 有关详细信息，请参阅[保护连接信息](../../data/adonet/protecting-connection-information.md)。  
  
### <a name="to-filter-data-with-the-bindingsource"></a>若要使用 BindingSource 的数据进行筛选  
  
-   设置<xref:System.Windows.Forms.BindingSource.Filter%2A>属性设置为所需的表达式。  
  
     在下面的代码示例，该表达式是列名称后跟所需的列的值。  
  
 [!code-csharp[System.Windows.Forms.DataConnectorFilterAndSort#11](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorFilterAndSort/CS/form1.cs#11)]
 [!code-vb[System.Windows.Forms.DataConnectorFilterAndSort#11](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorFilterAndSort/VB/form1.vb#11)]  
  
### <a name="to-sort-data-with-the-bindingsource"></a>使用 BindingSource 的数据进行排序  
  
1.  设置<xref:System.Windows.Forms.BindingSource.Sort%2A>属性设置为你想跟的列名称`ASC`或`DESC`以指示升序或降序排序。  
  
2.  请用逗号分隔多个列。  
  
 [!code-csharp[System.Windows.Forms.DataConnectorFilterAndSort#12](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorFilterAndSort/CS/form1.cs#12)]
 [!code-vb[System.Windows.Forms.DataConnectorFilterAndSort#12](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorFilterAndSort/VB/form1.vb#12)]  
  
## <a name="example"></a>示例  
 下面的代码示例将数据加载到 Northwind 示例数据库的 Customers 表从<xref:System.Windows.Forms.DataGridView>控制，并筛选，并对所显示的数据进行排序。  
  
 [!code-csharp[System.Windows.Forms.DataConnectorFilterAndSort#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorFilterAndSort/CS/form1.cs#1)]
 [!code-vb[System.Windows.Forms.DataConnectorFilterAndSort#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorFilterAndSort/VB/form1.vb#1)]  
  
## <a name="compiling-the-code"></a>编译代码  
 若要运行此示例，请将代码粘贴到包含一个窗体<xref:System.Windows.Forms.BindingSource>名为`BindingSource1`和一个<xref:System.Windows.Forms.DataGridView>名为`dataGridView1`。 处理<xref:System.Windows.Forms.Form.Load>窗体和调用事件`InitializeSortedFilteredBindingSource`load 事件处理程序方法中。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.BindingSource.Sort%2A>
- <xref:System.Windows.Forms.BindingSource.Filter%2A>
- [如何：安装示例数据库](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/8b6y4c7s(v=vs.120))
- [BindingSource 组件](bindingsource-component.md)
