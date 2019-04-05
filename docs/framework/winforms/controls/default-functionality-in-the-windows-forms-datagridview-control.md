---
title: Windows 窗体 DataGridView 控件中的默认功能
ms.date: 03/30/2017
helpviewer_keywords:
- data grids [Windows Forms], default functionality in DataGridView control
- DataGridView control [Windows Forms], default functionality
ms.assetid: 4405f697-cad1-4839-9bcd-8ddb09d9f00e
ms.openlocfilehash: 0c0d24111a2fdf856ff1f4ce154ec85afbbd61ee
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57719658"
---
# <a name="default-functionality-in-the-windows-forms-datagridview-control"></a>Windows 窗体 DataGridView 控件中的默认功能
Windows 窗体<xref:System.Windows.Forms.DataGridView>控件为用户提供了大量的默认功能。  
  
## <a name="default-functionality"></a>默认功能  
 默认情况下，<xref:System.Windows.Forms.DataGridView>控件：  
  
-   会自动显示列标题和行标题的垂直滚动表时保持可见。  
  
-   具有行标题，其中包含当前行的选择指示器。  
  
-   第一个单元格中具有选择矩形。  
  
-   包含可以自动调整大小以当用户双击的列分隔条的列。  
  
-   自动支持在 Windows XP 和 Windows Server 2003 系列上的视觉样式时<xref:System.Windows.Forms.Application.EnableVisualStyles%2A>方法从应用程序的调用`Main`方法。  
  
 此外的内容<xref:System.Windows.Forms.DataGridView>默认情况下，可以编辑控件：  
  
-   如果用户双击或按 F2 单元中的，该控件将自动使单元格进入编辑模式，并更新的单元格的内容与用户类型。  
  
-   如果用户滚动到网格的末尾时，用户将看到用于添加新记录的行是否存在。 当用户单击此行时，新行添加到<xref:System.Windows.Forms.DataGridView>控件，具有默认值。 当用户按 esc 键时，此新行将消失。  
  
-   如果用户单击行标题，则选择整个行。  
  
 当绑定<xref:System.Windows.Forms.DataGridView>控件与数据源通过设置其<xref:System.Windows.Forms.DataGridView.DataSource%2A>属性、 控件：  
  
-   自动使用的数据源的列的名称作为列标题文本。  
  
-   使用数据源的内容填充。 <xref:System.Windows.Forms.DataGridView> 对于每个列的数据源中自动创建列。  
  
-   在表中创建每个可见行的行。  
  
-   自动对基于对基础数据，当用户单击列标题的行进行排序。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.DataGridView>
- [DataGridView 控件](datagridview-control-windows-forms.md)
