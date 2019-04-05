---
title: Windows 窗体 DataGridView 控件中的数据格式设置
ms.date: 03/30/2017
helpviewer_keywords:
- DataGridView control [Windows Forms], formatting data
- data [Windows Forms], formatting in grids
- data grids [Windows Forms], formatting data
ms.assetid: 07bf558d-3748-42ba-8ba0-37fdef924081
ms.openlocfilehash: 60fc567a700bdfc8cfe088f4d31a68fd5de9aa29
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57722043"
---
# <a name="data-formatting-in-the-windows-forms-datagridview-control"></a>Windows 窗体 DataGridView 控件中的数据格式设置
<xref:System.Windows.Forms.DataGridView>控件提供了单元格的值与父列显示的数据类型之间的自动转换。 文本中的列，例如，显示日期、 时间、 数字和枚举值的字符串表示形式，并将用户输入的字符串值转换为数据存储所需的类型。  
  
## <a name="formatting-with-the-datagridviewcellstyle-class"></a>使用 DataGridViewCellStyle 类进行格式设置  
 <xref:System.Windows.Forms.DataGridView>控件提供了基本的数据通过的单元值的格式设置<xref:System.Windows.Forms.DataGridViewCellStyle>类。 可以使用<xref:System.Windows.Forms.DataGridViewCellStyle.Format%2A>属性设置为当前使用中所述的格式说明符的默认区域性的格式日期、 时间、 数字和枚举值[格式设置类型](../../../standard/base-types/formatting-types.md)。 此外可以设置格式的特定区域性使用的这些值<xref:System.Windows.Forms.DataGridViewCellStyle.FormatProvider%2A>属性。 使用指定的格式来显示数据并分析用户输入中指定的格式的数据。  
  
 <xref:System.Windows.Forms.DataGridViewCellStyle>类提供其他格式设置属性的换行、 文本对齐方式和自定义显示的空数据库值。 有关详细信息，请参阅[如何：Windows 中的数据格式窗体 DataGridView 控件](how-to-format-data-in-the-windows-forms-datagridview-control.md)。  
  
## <a name="formatting-with-the-cellformatting-event"></a>使用 CellFormatting 事件进行格式设置  
 如果基本格式设置不满足您的需要，可以提供自定义数据的处理程序中的格式设置<xref:System.Windows.Forms.DataGridView.CellFormatting?displayProperty=nameWithType>事件。 <xref:System.Windows.Forms.DataGridViewCellFormattingEventArgs>传递到处理具有<xref:System.Windows.Forms.ConvertEventArgs.Value%2A>最初包含单元格的值的属性。 通常情况下，此值自动转换为显示类型中。 若要自行转换值，设置<xref:System.Windows.Forms.ConvertEventArgs.Value%2A>属性的显示类型的值。  
  
> [!NOTE]
>  如果单元格实际上是一个格式字符串，它将覆盖的更改<xref:System.Windows.Forms.ConvertEventArgs.Value%2A>属性值，除非您设置<xref:System.Windows.Forms.DataGridViewCellFormattingEventArgs.FormattingApplied%2A>属性设置为`true`。  
  
 <xref:System.Windows.Forms.DataGridView.CellFormatting>事件非常有用，当你想要设置<xref:System.Windows.Forms.DataGridViewCellStyle>单个单元格的属性基于它们的值。 有关详细信息，请参阅[如何：自定义 Windows 窗体 DataGridView 控件中的数据格式设置](how-to-customize-data-formatting-in-the-windows-forms-datagridview-control.md)。  
  
 如果用户指定的值的默认分析不满足你的需求，则可以处理<xref:System.Windows.Forms.DataGridView.CellParsing>事件的<xref:System.Windows.Forms.DataGridView>控件提供自定义分析。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridViewCellStyle>
- [在 Windows 窗体 DataGridView 控件中显示数据](displaying-data-in-the-windows-forms-datagridview-control.md)
- [Windows 窗体 DataGridView 控件中的单元格样式](cell-styles-in-the-windows-forms-datagridview-control.md)
- [如何：Windows 中的数据格式窗体 DataGridView 控件](how-to-format-data-in-the-windows-forms-datagridview-control.md)
- [如何：自定义 Windows 窗体 DataGridView 控件中的数据格式设置](how-to-customize-data-formatting-in-the-windows-forms-datagridview-control.md)
