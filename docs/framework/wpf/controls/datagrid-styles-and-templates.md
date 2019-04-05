---
title: DataGrid 样式和模板
ms.date: 03/30/2017
helpviewer_keywords:
- states [WPF], DataGrid
- ControlTemplate [WPF], DataGrid
- DataGrid [WPF], styles and templates
- templates [WPF], DataGrid
- styles [WPF], DataGrid
- parts [WPF], DataGrid
ms.assetid: 9cb31d63-f148-4d25-b079-816e73f988c7
ms.openlocfilehash: 582179d8469cabc3551e1bed53c87e045f26e7cf
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57366070"
---
# <a name="datagrid-styles-and-templates"></a>DataGrid 样式和模板
本主题介绍的样式和模板的<xref:System.Windows.Controls.DataGrid>控件。 可以修改默认<xref:System.Windows.Controls.ControlTemplate>为控件提供唯一外观。 有关详细信息，请参阅[通过创建 ControlTemplate 自定义现有控件的外观](customizing-the-appearance-of-an-existing-control.md)。  
  
## <a name="datagrid-parts"></a>DataGrid 部件  
 下表列出了用于命名的部件<xref:System.Windows.Controls.DataGrid>控件。  
  
|部件|类型|描述|  
|-|-|-|  
|PART_ColumnHeadersPresenter|<xref:System.Windows.Controls.Primitives.DataGridColumnHeadersPresenter>|包含列标题的行。|  
  
 当您创建<xref:System.Windows.Controls.ControlTemplate>有关<xref:System.Windows.Controls.DataGrid>，模板可能包含<xref:System.Windows.Controls.ItemsPresenter>内<xref:System.Windows.Controls.ScrollViewer>。 (<xref:System.Windows.Controls.ItemsPresenter>显示在每个项<xref:System.Windows.Controls.DataGrid>;<xref:System.Windows.Controls.ScrollViewer>控件内实现滚动)。  如果<xref:System.Windows.Controls.ItemsPresenter>不是直接子级<xref:System.Windows.Controls.ScrollViewer>，必须授予<xref:System.Windows.Controls.ItemsPresenter>名称， `ItemsPresenter`。  
  
 默认模板<xref:System.Windows.Controls.DataGrid>包含<xref:System.Windows.Controls.ScrollViewer>控件。 有关定义的部件的详细信息<xref:System.Windows.Controls.ScrollViewer>，请参阅[ScrollViewer 样式和模板](scrollviewer-styles-and-templates.md)。  
  
## <a name="datagrid-states"></a>数据网格状态  
 下表列出了的可视状态<xref:System.Windows.Controls.DataGrid>控件。  
  
|VisualState 名称|VisualStateGroup 名称|描述|  
|-|-|-|  
|普通|CommonStates|默认状态。|  
|已禁用|CommonStates|已禁用控件。|  
|InvalidFocused|ValidationStates|控件无效，但具有焦点。|  
|InvalidUnfocused|ValidationStates|控件无效，并且没有焦点。|  
|有效|ValidationStates|控件有效。|  
  
## <a name="datagridcell-parts"></a>DataGridCell 部件  
 <xref:System.Windows.Controls.DataGridCell>元素不具有任何命名的部件。  
  
## <a name="datagridcell-states"></a>DataGridCell 状态  
 下表列出了的可视状态<xref:System.Windows.Controls.DataGridCell>元素。  
  
|VisualState 名称|VisualStateGroup 名称|描述|  
|-|-|-|  
|普通|CommonStates|默认状态。|  
|MouseOver|CommonStates|鼠标指针置于单元格。|  
|已设定焦点|FocusStates|该单元格有焦点。|  
|失去焦点|FocusStates|该单元格不具有焦点|  
|当前|CurrentStates|该单元格是当前单元格。|  
|规则|CurrentStates|该单元格不是当前单元格。|  
|显示|InteractionStates|该单元格位于显示模式。|  
|编辑|InteractionStates|该单元格处于编辑模式。|  
|已选定|SelectionStates|选定该单元格。|  
|未选定|SelectionStates|未选择该单元格。|  
|InvalidFocused|ValidationStates|该单元格无效，且具有焦点。|  
|InvalidUnfocused|ValidationStates|该单元格无效，不具有焦点。|  
|有效|ValidationStates|该单元格是有效的。|  
  
## <a name="datagridrow-parts"></a>DataGridRow 部件  
 <xref:System.Windows.Controls.DataGridRow>元素不具有任何命名的部件。  
  
## <a name="datagridrow-states"></a>DataGridRow 状态  
 下表列出了的可视状态<xref:System.Windows.Controls.DataGridRow>元素。  
  
|VisualState 名称|VisualStateGroup 名称|描述|  
|-|-|-|  
|普通|CommonStates|默认状态。|  
|MouseOver|CommonStates|鼠标指针置于行。|  
|MouseOver_Editing|CommonStates|鼠标指针置于行和行处于编辑模式。|  
|MouseOver_Selected|CommonStates|鼠标指针置于该行并选择的行。|  
|MouseOver_Unfocused_Editing|CommonStates|鼠标指针置于行、 行处于编辑模式，并且不具有焦点。|  
|MouseOver_Unfocused_Selected|CommonStates|鼠标指针置于行，行选择，则并不具有焦点。|  
|Normal_AlternatingRow|CommonStates|行是交替行。|  
|Normal_Editing|CommonStates|行处于编辑模式。|  
|Normal_Selected|CommonStates|选择的行。|  
|Unfocused_Editing|CommonStates|行处于编辑模式并不具有焦点。|  
|Unfocused_Selected|CommonStates|行处于选中状态，并且不具有焦点。|  
|InvalidFocused|ValidationStates|控件无效，但具有焦点。|  
|InvalidUnfocused|ValidationStates|控件无效，并且没有焦点。|  
|有效|ValidationStates|控件有效。|  
  
## <a name="datagridrowheader-parts"></a>DataGridRowHeader 部件  
 下表列出了用于命名的部件<xref:System.Windows.Controls.Primitives.DataGridRowHeader>元素。  
  
|部件|类型|描述|  
|-|-|-|  
|PART_TopHeaderGripper|<xref:System.Windows.Controls.Primitives.Thumb>|用于调整行标题顶部的元素。|  
|PART_BottomHeaderGripper|<xref:System.Windows.Controls.Primitives.Thumb>|用于调整大小从底部的行标头元素。|  
  
## <a name="datagridrowheader-states"></a>DataGridRowHeader 状态  
 下表列出了的可视状态<xref:System.Windows.Controls.Primitives.DataGridRowHeader>元素。  
  
|VisualState 名称|VisualStateGroup 名称|描述|  
|-|-|-|  
|普通|CommonStates|默认状态。|  
|MouseOver|CommonStates|鼠标指针置于行。|  
|MouseOver_CurrentRow|CommonStates|鼠标指针定位的行，该行是当前行。|  
|MouseOver_CurrentRow_Selected|CommonStates|鼠标指针置于行，并且行是当前和所选。|  
|MouseOver_EditingRow|CommonStates|鼠标指针置于行和行处于编辑模式。|  
|MouseOver_Selected|CommonStates|鼠标指针置于该行并选择的行。|  
|MouseOver_Unfocused_CurrentRow_Selected|CommonStates|鼠标指针置于一行，该行当前和选择，并不具有焦点。|  
|MouseOver_Unfocused_EditingRow|CommonStates|鼠标指针置于行、 行处于编辑模式，并且不具有焦点。|  
|MouseOver_Unfocused_Selected|CommonStates|鼠标指针置于行，行选择，则并不具有焦点。|  
|Normal_CurrentRow|CommonStates|行是当前行。|  
|Normal_CurrentRow_Selected|CommonStates|行是当前行，并且处于选中状态。|  
|Normal_EditingRow|CommonStates|行处于编辑模式。|  
|Normal_Selected|CommonStates|选择的行。|  
|Unfocused_CurrentRow_Selected|CommonStates|行是当前行，被选定，并且不具有焦点。|  
|Unfocused_EditingRow|CommonStates|行处于编辑模式并不具有焦点。|  
|Unfocused_Selected|CommonStates|行处于选中状态，并且不具有焦点。|  
|InvalidFocused|ValidationStates|控件无效，但具有焦点。|  
|InvalidUnfocused|ValidationStates|控件无效，并且没有焦点。|  
|有效|ValidationStates|控件有效。|  
  
## <a name="datagridcolumnheaderspresenter-parts"></a>DataGridColumnHeadersPresenter 部件  
 下表列出了用于命名的部件<xref:System.Windows.Controls.Primitives.DataGridColumnHeadersPresenter>元素。  
  
|部件|类型|描述|  
|-|-|-|  
|PART_FillerColumnHeader|<xref:System.Windows.Controls.Primitives.DataGridColumnHeader>|列标题的占位符。|  
  
## <a name="datagridcolumnheaderspresenter-states"></a>DataGridColumnHeadersPresenter States  
 下表列出了的可视状态<xref:System.Windows.Controls.Primitives.DataGridColumnHeadersPresenter>元素。  
  
|VisualState 名称|VisualStateGroup 名称|描述|  
|-|-|-|  
|InvalidFocused|ValidationStates|该单元格无效，且具有焦点。|  
|InvalidUnfocused|ValidationStates|该单元格无效，不具有焦点。|  
|有效|ValidationStates|该单元格是有效的。|  
  
## <a name="datagridcolumnheader-parts"></a>DataGridColumnHeader 部件  
 下表列出了用于命名的部件<xref:System.Windows.Controls.Primitives.DataGridColumnHeader>元素。  
  
|部件|类型|描述|  
|-|-|-|  
|PART_LeftHeaderGripper|<xref:System.Windows.Controls.Primitives.Thumb>|用于调整大小从左侧的列标题元素。|  
|PART_RightHeaderGripper|<xref:System.Windows.Controls.Primitives.Thumb>|用于调整大小从右侧的列标题元素。|  
  
## <a name="datagridcolumnheader-states"></a>DataGridColumnHeader 状态  
 下表列出了的可视状态<xref:System.Windows.Controls.Primitives.DataGridColumnHeader>元素。  
  
|VisualState 名称|VisualStateGroup 名称|描述|  
|-|-|-|  
|普通|CommonStates|默认状态。|  
|MouseOver|CommonStates|鼠标指针悬停在控件上方。|  
|已按下|CommonStates|已按下控件。|  
|SortAscending|SortStates|对列按升序进行排序。|  
|SortDescending|SortStates|对列进行降序排序。|  
|未排序|SortStates|未对列进行排序。|  
|InvalidFocused|ValidationStates|控件无效，但具有焦点。|  
|InvalidUnfocused|ValidationStates|控件无效，并且没有焦点。|  
|有效|ValidationStates|控件有效。|  
  
## <a name="datagrid-controltemplate-example"></a>DataGrid ControlTemplate 示例  
 下面的示例演示如何定义<xref:System.Windows.Controls.ControlTemplate>为<xref:System.Windows.Controls.DataGrid>控件和其关联的类型。  
  
 [!code-xaml[ControlTemplateExamples#DataGrid](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/datagrid.xaml#datagrid)]  
  
 上一示例使用了一个或多个以下资源。  
  
 [!code-xaml[ControlTemplateExamples#Resources](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/shared.xaml#resources)]  
  
 有关完整示例，请参阅[使用 ControlTemplates 设置样式示例](https://github.com/Microsoft/WPF-Samples/tree/master/Styles%20&%20Templates/IntroToStylingAndTemplating)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.FrameworkElement.Style%2A>
- <xref:System.Windows.Controls.ControlTemplate>
- [控件样式和模板](control-styles-and-templates.md)
- [控件自定义](control-customization.md)
- [样式设置和模板化](styling-and-templating.md)
- [通过创建 ControlTemplate 自定义现有控件的外观](customizing-the-appearance-of-an-existing-control.md)
