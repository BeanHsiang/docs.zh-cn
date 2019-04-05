---
title: Windows 窗体 DataGridView 控件中的单元格样式
ms.date: 03/30/2017
helpviewer_keywords:
- DataGridView control [Windows Forms], cell styles
- cells [Windows Forms], styles
- data grids [Windows Forms], cell styles
ms.assetid: dbb75ed6-8804-4232-8382-f9920c2e380c
ms.openlocfilehash: a22fc29d2cab21977c0411a440b847b426fb5915
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57712265"
---
# <a name="cell-styles-in-the-windows-forms-datagridview-control"></a>Windows 窗体 DataGridView 控件中的单元格样式
中的每个单元格<xref:System.Windows.Forms.DataGridView>控件可以有自己的样式，如文本格式、 背景色、 前景色和字体。 但是，通常情况下，多个单元格将共享特定的样式特征。  
  
 共享样式的单元格的组可能会在控件中包括特定的行或列、 包含特定值的所有单元格或所有单元格内的所有单元格。 因为这些组重叠，则每个单元格可能从多个位置中获取其样式信息。 例如，可能希望每个单元格<xref:System.Windows.Forms.DataGridView>使用带有负数的相同字体，但仅中要使用货币格式的货币列的单元格和仅货币单元格，才能使用红色前景颜色的控件。  
  
## <a name="the-datagridviewcellstyle-class"></a>DataGridViewCellStyle 类  
 <xref:System.Windows.Forms.DataGridViewCellStyle>类包含视觉样式相关的以下属性：  
  
-   <xref:System.Windows.Forms.DataGridViewCellStyle.BackColor%2A> 和 <xref:System.Windows.Forms.DataGridViewCellStyle.ForeColor%2A>  
  
-   <xref:System.Windows.Forms.DataGridViewCellStyle.SelectionBackColor%2A> 和 <xref:System.Windows.Forms.DataGridViewCellStyle.SelectionForeColor%2A>  
  
-   <xref:System.Windows.Forms.DataGridViewCellStyle.Font%2A>  
  
 此类还包含与格式设置相关的以下属性：  
  
-   <xref:System.Windows.Forms.DataGridViewCellStyle.Format%2A> 和 <xref:System.Windows.Forms.DataGridViewCellStyle.FormatProvider%2A>  
  
-   <xref:System.Windows.Forms.DataGridViewCellStyle.NullValue%2A> 和 <xref:System.Windows.Forms.DataGridViewCellStyle.DataSourceNullValue%2A>  
  
-   <xref:System.Windows.Forms.DataGridViewCellStyle.WrapMode%2A>  
  
-   <xref:System.Windows.Forms.DataGridViewCellStyle.Alignment%2A>  
  
-   <xref:System.Windows.Forms.DataGridViewCellStyle.Padding%2A>  
  
 有关这些属性和其他单元格样式属性的详细信息，请参阅<xref:System.Windows.Forms.DataGridViewCellStyle>下面的另请参见部分中列出的参考文档和主题。  
  
## <a name="using-datagridviewcellstyle-objects"></a>使用 DataGridViewCellStyle 对象  
 可以检索<xref:System.Windows.Forms.DataGridViewCellStyle>中的各种属性的对象<xref:System.Windows.Forms.DataGridView>， <xref:System.Windows.Forms.DataGridViewColumn>， <xref:System.Windows.Forms.DataGridViewRow>，和<xref:System.Windows.Forms.DataGridViewCell>类和其派生的类。 如果这些属性之一具有尚未设置，检索其值会创建一个新<xref:System.Windows.Forms.DataGridViewCellStyle>对象。 您还可以实例化自己<xref:System.Windows.Forms.DataGridViewCellStyle>对象，并将其分配给这些属性。  
  
 您可以通过共享来避免不必要地重复的样式信息<xref:System.Windows.Forms.DataGridViewCellStyle>多个对象<xref:System.Windows.Forms.DataGridView>元素。 由于样式设置在控件、 列和行级别筛选器下通过到单元格级别的每个级别，因此还可以通过在不同于上面的级别每个级别设置只显示那些样式属性来避免样式重复。 这是在后面的样式继承部分中的更多详细信息中所述。  
  
 下表列出了用于获取或设置主属性<xref:System.Windows.Forms.DataGridViewCellStyle>对象。  
  
|属性|类|描述|  
|--------------|-------------|-----------------|  
|`DefaultCellStyle`|<xref:System.Windows.Forms.DataGridView><xref:System.Windows.Forms.DataGridViewColumn>， <xref:System.Windows.Forms.DataGridViewRow>，和派生类|获取或设置使用在整个控件 （包括标题单元格），在列中，或行中的所有单元格的默认样式。|  
|<xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A>|<xref:System.Windows.Forms.DataGridView>|获取或设置使用的控件中的所有行的默认单元格样式。 这不包括标头单元格。|  
|<xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A>|<xref:System.Windows.Forms.DataGridView>|获取或设置交替行控件中的使用的默认单元格样式。 用于创建类似于分类帐的效果。|  
|<xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle%2A>|<xref:System.Windows.Forms.DataGridView>|获取或设置使用的控件的行标题的默认单元格样式。 如果启用了可视样式，替代当前主题。|  
|<xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A>|<xref:System.Windows.Forms.DataGridView>|获取或设置使用的控件的列标题的默认单元格样式。 如果启用了可视样式，替代当前主题。|  
|<xref:System.Windows.Forms.DataGridViewCell.Style%2A>|<xref:System.Windows.Forms.DataGridViewCell> 派生类|获取或设置单元格级别指定的样式。 这些样式会覆盖从较高级别继承。|  
|`InheritedStyle`|<xref:System.Windows.Forms.DataGridViewCell><xref:System.Windows.Forms.DataGridViewRow>， <xref:System.Windows.Forms.DataGridViewColumn>，和派生类|获取当前应用于单元格、 行或列，其中包括从较高级别继承的所有样式。|  
  
 如上所述，自动获取样式属性的值实例化新<xref:System.Windows.Forms.DataGridViewCellStyle>对象如果属性尚未之前设置。 若要避免不必要地创建这些对象，在行和列类具有<xref:System.Windows.Forms.DataGridViewBand.HasDefaultCellStyle%2A>属性，您可以通过检查来确定是否<xref:System.Windows.Forms.DataGridViewBand.DefaultCellStyle%2A>设置属性。 同样，单元格类具有<xref:System.Windows.Forms.DataGridViewCell.HasStyle%2A>属性，指示是否<xref:System.Windows.Forms.DataGridViewCell.Style%2A>设置属性。  
  
 样式属性的每个都有相应*PropertyName* `Changed`上的事件<xref:System.Windows.Forms.DataGridView>控件。 有关行、 列和单元属性，该事件的名称开头"`Row`"，"`Column`"，或"`Cell`"(例如， <xref:System.Windows.Forms.DataGridView.RowDefaultCellStyleChanged>)。 每个事件发生时相应的样式属性设置为另一种<xref:System.Windows.Forms.DataGridViewCellStyle>对象。 在检索时不会发生这些事件<xref:System.Windows.Forms.DataGridViewCellStyle>对象从一个样式属性，并修改其属性值。 若要对单元格样式对象本身的更改做出响应，处理<xref:System.Windows.Forms.DataGridView.CellStyleContentChanged>事件。  
  
## <a name="style-inheritance"></a>样式继承  
 每个<xref:System.Windows.Forms.DataGridViewCell>获取从其外观其<xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A>属性。 <xref:System.Windows.Forms.DataGridViewCellStyle>此属性返回的对象继承其属性值的类型的属性层次结构从<xref:System.Windows.Forms.DataGridViewCellStyle>。 下面列出的顺序在这些属性<xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A>非标头单元格获得其值。  
  
1.  <xref:System.Windows.Forms.DataGridViewCell.Style%2A?displayProperty=nameWithType>  
  
2.  <xref:System.Windows.Forms.DataGridViewRow.DefaultCellStyle%2A?displayProperty=nameWithType>  
  
3.  <xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A?displayProperty=nameWithType> （仅适用于具有奇数的索引号的行中单元格）  
  
4.  <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A?displayProperty=nameWithType>  
  
5.  <xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A?displayProperty=nameWithType>  
  
6.  <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType>  
  
 为行和列标题单元格<xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A>用从以下列表按给定顺序的源属性的值填充属性。  
  
1.  <xref:System.Windows.Forms.DataGridViewCell.Style%2A?displayProperty=nameWithType>  
  
2.  <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A?displayProperty=nameWithType> 或 <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle%2A?displayProperty=nameWithType>  
  
3.  <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType>  
  
 下图说明了此过程。  
  
 ![类型 DataGridViewCellStyle 的属性](./media/cell-styles-in-the-windows-forms-datagridview-control/datagridviewcells-inheritance-diagram.gif "DataGridViewCells 继承关系图")  
  
 此外可以访问继承的特定行和列的样式。 列<xref:System.Windows.Forms.DataGridViewColumn.InheritedStyle%2A>属性从下列属性继承它的值。  
  
1.  <xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A?displayProperty=nameWithType>  
  
2.  <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType>  
  
 行<xref:System.Windows.Forms.DataGridViewRow.InheritedStyle%2A>属性从下列属性继承它的值。  
  
1.  <xref:System.Windows.Forms.DataGridViewRow.DefaultCellStyle%2A?displayProperty=nameWithType>  
  
2.  <xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A?displayProperty=nameWithType> （仅适用于具有奇数的索引号的行中单元格）  
  
3.  <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A?displayProperty=nameWithType>  
  
4.  <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType>  
  
 中每个属性<xref:System.Windows.Forms.DataGridViewCellStyle>返回的对象`InheritedStyle`属性，属性值从第一个单元格样式在相应的列表具有相应的属性设置为一个值，而不获取<xref:System.Windows.Forms.DataGridViewCellStyle>类的默认值。  
  
 下表说明了如何将<xref:System.Windows.Forms.DataGridViewCellStyle.ForeColor%2A>示例单元格的属性值继承自其包含的列。  
  
|类型的属性 `DataGridViewCellStyle`|示例`ForeColor`检索到的对象的值|  
|----------------------------------------------|----------------------------------------------------|  
|<xref:System.Windows.Forms.DataGridViewCell.Style%2A?displayProperty=nameWithType>|<xref:System.Drawing.Color.Empty?displayProperty=nameWithType>|  
|<xref:System.Windows.Forms.DataGridViewRow.DefaultCellStyle%2A?displayProperty=nameWithType>|<xref:System.Drawing.Color.Red%2A?displayProperty=nameWithType>|  
|<xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A?displayProperty=nameWithType>|<xref:System.Drawing.Color.Empty?displayProperty=nameWithType>|  
|<xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A?displayProperty=nameWithType>|<xref:System.Drawing.Color.Empty?displayProperty=nameWithType>|  
|<xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A?displayProperty=nameWithType>|<xref:System.Drawing.Color.DarkBlue%2A?displayProperty=nameWithType>|  
|<xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType>|<xref:System.Drawing.Color.Black%2A?displayProperty=nameWithType>|  
  
 在这种情况下，<xref:System.Drawing.Color.Red%2A?displayProperty=nameWithType>从单元格的行的值是列表上的第一个实际值。 这将成为<xref:System.Windows.Forms.DataGridViewCellStyle.ForeColor%2A>属性值的单元格的<xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A>。  
  
 下图说明了如何将不同<xref:System.Windows.Forms.DataGridViewCellStyle>属性继承其属性值从不同的位置。  
  
 ![DataGridView 属性&#45;值继承](./media/cell-styles-in-the-windows-forms-datagridview-control/datagridviewcells-value-inheritance-diagram.gif "DataGridViewCells 值继承关系图")  
  
 通过利用样式继承，可以为整个控件提供适当的样式，而无需在多个位置指定相同的信息。  
  
 尽管标头单元格参与样式继承，如所述，通过返回的对象<xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A>并<xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle%2A>的属性<xref:System.Windows.Forms.DataGridView>控件具有重写返回的对象的属性值的初始属性值<xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A>属性。 如果您要返回的对象设置属性<xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A>属性应用到行和列标题，必须设置返回的对象的相应属性<xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A>和<xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle%2A>所指示的默认值的属性有关<xref:System.Windows.Forms.DataGridViewCellStyle>类。  
  
> [!NOTE]
>  如果启用了可视样式，行和列标题 (除<xref:System.Windows.Forms.DataGridView.TopLeftHeaderCell%2A>) 样式将自动由当前主题，重写这些属性指定任何样式。  
  
 <xref:System.Windows.Forms.DataGridViewButtonColumn>， <xref:System.Windows.Forms.DataGridViewImageColumn>，并<xref:System.Windows.Forms.DataGridViewCheckBoxColumn>类型还初始化的列返回的对象的某些值<xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A>属性。 有关详细信息，请参阅这些类型的参考文档。  
  
## <a name="setting-styles-dynamically"></a>动态设置样式  
 若要自定义的具有特定值的单元格的样式，实现的处理程序<xref:System.Windows.Forms.DataGridView.CellFormatting?displayProperty=nameWithType>事件。 此事件处理程序接收的自变量<xref:System.Windows.Forms.DataGridViewCellFormattingEventArgs>类型。 此对象包含属性，可确定其位置以及要设置格式的单元格的值<xref:System.Windows.Forms.DataGridView>控件。 此对象还包含<xref:System.Windows.Forms.DataGridViewCellFormattingEventArgs.CellStyle%2A>初始化为的值的属性<xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A>正在格式化的单元格的属性。 可以修改的单元格样式属性来指定相应的单元格的值和位置的样式信息。  
  
> [!NOTE]
>  <xref:System.Windows.Forms.DataGridView.RowPrePaint>并<xref:System.Windows.Forms.DataGridView.RowPostPaint>事件也会收到<xref:System.Windows.Forms.DataGridViewCellStyle>对象在事件数据，但在其大小写，它是行的副本<xref:System.Windows.Forms.DataGridViewRow.InheritedStyle%2A>属性用于只读目的并对它的更改不会影响该控件。  
  
 如还可以动态修改响应事件的各个单元格的样式<xref:System.Windows.Forms.DataGridView.CellMouseEnter?displayProperty=nameWithType>和<xref:System.Windows.Forms.DataGridView.CellMouseLeave>事件。 例如，在处理程序<xref:System.Windows.Forms.DataGridView.CellMouseEnter>事件，可以存储的单元格背景色的当前值 (通过该单元格的检索<xref:System.Windows.Forms.DataGridViewCell.Style%2A>属性)，然后将其设置为将突出显示该单元格，当鼠标悬停时的新颜色。 中的处理程序<xref:System.Windows.Forms.DataGridView.CellMouseLeave>事件，然后将背景色还原为原始值。  
  
> [!NOTE]
>  缓存存储在单元格的值<xref:System.Windows.Forms.DataGridViewCell.Style%2A>属性是非常重要，而不考虑是否设置了特定样式值。 如果您暂时替换样式设置，将其还原到其原始的"未设置"状态可确保，则该单元格将返回到从高级别继承的样式设置。 如果您需要确定有效的而不考虑是否继承样式的单元格的实际样式，使用该单元格的<xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A>属性。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridViewCellStyle>
- <xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewBand.InheritedStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewRow.InheritedStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewColumn.InheritedStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewBand.DefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewCell.Style%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.CellFormatting?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.CellStyleContentChanged?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.RowPrePaint?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.RowPostPaint?displayProperty=nameWithType>
- [Windows 窗体 DataGridView 控件中的基本格式和样式设置](basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)
- [如何：设置 Windows 窗体 DataGridView 控件的默认单元格样式](how-to-set-default-cell-styles-for-the-windows-forms-datagridview-control.md)
- [Windows 窗体 DataGridView 控件中的数据格式设置](data-formatting-in-the-windows-forms-datagridview-control.md)
