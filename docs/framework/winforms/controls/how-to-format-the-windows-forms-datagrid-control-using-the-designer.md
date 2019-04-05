---
title: 如何：设置 Windows 窗体 DataGrid 控件使用设计器的格式
ms.date: 03/30/2017
helpviewer_keywords:
- columns [Windows Forms], DataGrid controls
- colors [Windows Forms], applying to DataGrid controls
- DataGrid control [Windows Forms], formatting
- DataGrid control [Windows Forms], default styles
- tables [Windows Forms], formatting in DataGrid control
- formatting [Windows Forms]
ms.assetid: 533b9814-6124-49dc-9fda-085f1502609f
ms.openlocfilehash: 92939f1bdddaca1d743116a4ae4ee9da657abf19
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57725358"
---
# <a name="how-to-format-the-windows-forms-datagrid-control-using-the-designer"></a>如何：设置 Windows 窗体 DataGrid 控件使用设计器的格式

> [!NOTE]
>  
  <xref:System.Windows.Forms.DataGridView> 控件取代了 <xref:System.Windows.Forms.DataGrid> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.DataGrid> 控件以实现向后兼容并供将来使用。 有关详细信息，请参阅 [Windows 窗体 DataGridView 控件与 DataGrid 控件之间的区别](differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)。  
  
 将不同的颜色应用到的各个部分<xref:System.Windows.Forms.DataGrid>控件来帮助简化在它的信息更轻松地阅读和理解。 颜色可以应用于行和列。 行和列可以还显示或隐藏您自行决定。  
  
 有三个基本方面的格式设置<xref:System.Windows.Forms.DataGrid>控件：  
  
-   您可以设置属性来建立数据显示为默认样式。  
  
-   以此为基础，你可以然后自定义在运行时显示某些表的方式。  
  
-   最后，您可以修改哪些列显示在数据网格和颜色，并显示了其他格式设置。  
  
 作为在格式设置数据网格中的初始步骤，可以设置的属性<xref:System.Windows.Forms.DataGrid>本身。 这些颜色和格式选择窗体从其然后可以进行更改，具体取决于数据的表和列显示的基础。  
  
 下面的过程需要**Windows 应用程序**包含一个窗体，其中包含项目<xref:System.Windows.Forms.DataGrid>控件。 有关设置此类项目的信息，请参阅[如何：创建 Windows 窗体应用程序项目](/visualstudio/ide/step-1-create-a-windows-forms-application-project)和[如何：将控件添加到 Windows 窗体](how-to-add-controls-to-windows-forms.md)。 在 Visual Studio 2005 中，<xref:System.Windows.Forms.DataGrid>控件不在**工具箱**默认情况下。 有关详细信息，请参阅[如何：将项添加到工具箱](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms165355(v=vs.100))。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
### <a name="to-establish-a-default-style-for-the-datagrid-control"></a>若要建立的 DataGrid 控件的默认样式  
  
1.  选择 <xref:System.Windows.Forms.DataGrid> 控件。  
  
2.  在中**属性**窗口中，根据需要设置以下属性。  
  
    |属性|描述|  
    |--------------|-----------------|  
    |<xref:System.Windows.Forms.DataGrid.AlternatingBackColor%2A>|`BackColor`属性定义的网格中偶数行的颜色。 当您将设置<xref:System.Windows.Forms.DataGrid.AlternatingBackColor%2A>为不同的颜色的属性，所有其他行设置为此新的颜色 （行 1、 3、 5 和等等）。|  
    |<xref:System.Windows.Forms.DataGrid.BackColor%2A>|在网格中偶数的行的背景色 （0、 2、 4、 6 和等等的行）。|  
    |<xref:System.Windows.Forms.DataGrid.BackgroundColor%2A>|而<xref:System.Windows.Forms.DataGrid.BackColor%2A>并<xref:System.Windows.Forms.DataGrid.AlternatingBackColor%2A>属性确定在网格中，行的颜色<xref:System.Windows.Forms.DataGrid.BackgroundColor%2A>属性确定的行区域，该网格中滚动到底部，或如果只有少量的行才可见区域之外区域的颜色包含在网格中。|  
    |<xref:System.Windows.Forms.DataGrid.BorderStyle%2A>|网格的边框样式，其中一个<xref:System.Windows.Forms.BorderStyle>枚举值。|  
    |<xref:System.Windows.Forms.DataGrid.CaptionBackColor%2A>|正上方网格的网格窗口标题的背景色。|  
    |<xref:System.Windows.Forms.DataGrid.CaptionFont%2A>|在网格的顶部的标题的字体。|  
    |<xref:System.Windows.Forms.DataGrid.CaptionForeColor%2A>|网格的窗口标题的背景色。|  
    |<xref:System.Windows.Forms.Control.Font%2A>|用于在网格中显示文本的字体。|  
    |<xref:System.Windows.Forms.DataGrid.ForeColor%2A>|数据网格行中的数据所显示的字体颜色。|  
    |<xref:System.Windows.Forms.DataGrid.GridLineColor%2A>|数据网格的网格线的颜色。|  
    |<xref:System.Windows.Forms.DataGrid.GridLineStyle%2A>|网格中的一个单元格进行分隔线的样式<xref:System.Windows.Forms.DataGridLineStyle>枚举值。|  
    |<xref:System.Windows.Forms.DataGrid.HeaderBackColor%2A>|行和列标题的背景色。|  
    |<xref:System.Windows.Forms.DataGrid.HeaderFont%2A>|用于列标题的字体。|  
    |<xref:System.Windows.Forms.DataGrid.HeaderForeColor%2A>|显示网格的列的标头，包括列标题文本的加号 （+） 和减号 （-） 标志符号的展开和折叠行时有多个相关表的前景色。|  
    |<xref:System.Windows.Forms.DataGrid.LinkColor%2A>|在数据网格中，其中包括指向子表、 关系名称和等等的所有链接的文本的颜色。|  
    |<xref:System.Windows.Forms.DataGrid.ParentRowsBackColor%2A>|在子表中，这是父行的背景色。|  
    |<xref:System.Windows.Forms.DataGrid.ParentRowsForeColor%2A>|在子表中，这是父行的前景色。|  
    |<xref:System.Windows.Forms.DataGrid.ParentRowsLabelStyle%2A>|确定表和列名称在父行中，通过显示<xref:System.Windows.Forms.DataGridParentRowsLabelStyle>枚举。|  
    |<xref:System.Windows.Forms.DataGrid.PreferredColumnWidth%2A>|网格中列的默认宽度（以像素为单位）。 设置此属性才能重置<xref:System.Windows.Forms.DataGrid.DataSource%2A>和<xref:System.Windows.Forms.DataGrid.DataMember%2A>属性 (可以单独或通过<xref:System.Windows.Forms.DataGrid.SetDataBinding%2A>方法)，或者该属性将不起作用。<br /><br /> 属性不能设置为小于 0 的值。|  
    |<xref:System.Windows.Forms.DataGrid.PreferredRowHeight%2A>|行的高度 （以像素为单位） 的网格中的行。 设置此属性才能重置<xref:System.Windows.Forms.DataGrid.DataSource%2A>和<xref:System.Windows.Forms.DataGrid.DataMember%2A>属性 (可以单独或通过<xref:System.Windows.Forms.DataGrid.SetDataBinding%2A>方法)，或者该属性将不起作用。<br /><br /> 属性不能设置为小于 0 的值。|  
    |<xref:System.Windows.Forms.DataGrid.RowHeaderWidth%2A>|网格的行标题的宽度。|  
    |<xref:System.Windows.Forms.DataGrid.SelectionBackColor%2A>|选择行或单元格后，这是背景色。|  
    |<xref:System.Windows.Forms.DataGrid.SelectionForeColor%2A>|选择行或单元格后，这是的前景色。|  
  
    > [!NOTE]
    >  当您要自定义控件的颜色时，就可以使控件无法访问，因为不佳的颜色选择 （例如，红色和绿色）。 使用提供的颜色**种系统颜色**调色板，若要避免此问题。

     下面的过程需要<xref:System.Windows.Forms.DataGrid>控件绑定到数据表。 有关详细信息，请参阅[如何：将 Windows 窗体 DataGrid 控件绑定到数据源](how-to-bind-the-windows-forms-datagrid-control-to-a-data-source.md)。

### <a name="to-set-the-table-and-column-style-of-a-data-table-at-design-time"></a>若要在设计时设置数据表的表和列样式

1.  选择<xref:System.Windows.Forms.DataGrid>窗体上的控件。

2.  在中**属性**窗口中，选择<xref:System.Windows.Forms.DataGrid.TableStyles%2A>属性，单击**省略号**(![VisualStudioEllipsesButton 屏幕快照](../media/vbellipsesbutton.png "vbEllipsesButton")) 按钮。

3.  在中**DataGridTableStyle 集合编辑器**对话框中，单击**添加**要添加到集合的表样式。

     与**DataGridTableStyle 集合编辑器**，可以添加和删除表样式，集显示和布局属性集的映射名称的表样式。

4.  设置<xref:System.Windows.Forms.DataGridTableStyle.MappingName%2A>属性设置为每个表样式的映射名称。

     映射名称用于指定应与表中的哪些表样式。

5.  在中**DataGridTableStyle 集合编辑器**，选择<xref:System.Windows.Forms.DataGridTableStyle.GridColumnStyles%2A>属性，然后单击省略号按钮 (![VisualStudioEllipsesButton 屏幕快照](../media/vbellipsesbutton.png "vbEllipsesButton")).

6.  在中**DataGridColumnStyle 集合编辑器**对话框框中，将列样式添加到你创建的表样式。

     与**DataGridColumnStyle 集合编辑器**，可以添加和删除列样式，设置显示和布局的属性，以及设置的映射名称和格式设置字符串的数据列。

    > [!NOTE]
    >  有关格式设置字符串的详细信息，请参阅[格式设置类型](../../../standard/base-types/formatting-types.md)。

## <a name="see-also"></a>请参阅

- <xref:System.Windows.Forms.GridTableStylesCollection>
- <xref:System.Windows.Forms.GridColumnStylesCollection>
- <xref:System.Windows.Forms.DataGrid>
- [如何：删除或隐藏 Windows 窗体 DataGrid 控件中的列](how-to-delete-or-hide-columns-in-the-windows-forms-datagrid-control.md)
- [DataGrid 控件](datagrid-control-windows-forms.md)