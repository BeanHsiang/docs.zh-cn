---
title: 如何：将数据绑定到使用设计器在 Windows 窗体 DataGridView 控件
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms controls, binding to a data source
- data sources [Windows Forms], binding to Windows Forms controls
- DataGridView control [Windows Forms], data binding
ms.assetid: f4f46009-cec2-441b-8668-6b5af057558b
ms.openlocfilehash: 8c90366111957f27a6bd86035013eba00426f46b
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57718501"
---
# <a name="how-to-bind-data-to-the-windows-forms-datagridview-control-using-the-designer"></a>如何：将数据绑定到使用设计器在 Windows 窗体 DataGridView 控件
可以使用设计器来连接<xref:System.Windows.Forms.DataGridView>不同种类的包括数据库、 业务对象或 Web 服务的数据源的控件。 当将控件绑定到数据源使用设计器中时，该控件自动绑定到<xref:System.Windows.Forms.BindingSource>表示数据源的组件。 此外，会在控件中自动生成列以匹配数据源提供的架构信息。  
  
 生成列后，可根据需要对其进行修改。 例如，可删除或隐藏不不想显示的列、重新排列各列或修改列的类型。 有关修改列的详细信息，请参阅“另请参阅”部分中列出的主题。  
  
 此外可以绑定多个<xref:System.Windows.Forms.DataGridView>控件添加到相关表来创建母版/详细信息的关系。 在此配置中，一个控件显示父表，另一个控件只显示子表中与父表中的当前行相关的行。 有关详细信息，请参阅[如何：在 Windows 中的数据窗体应用程序中显示相关](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/57tx3hhe(v=vs.120))。  
  
 下面的过程需要**Windows 应用程序**包含一个窗体项目<xref:System.Windows.Forms.DataGridView>控件或两个控件的母版/详细信息关系。 有关启动此类项目的信息，请参阅[如何：创建 Windows 窗体应用程序项目](/visualstudio/ide/step-1-create-a-windows-forms-application-project)和[如何：将控件添加到 Windows 窗体](how-to-add-controls-to-windows-forms.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
### <a name="to-bind-the-control-to-a-data-source"></a>将控件绑定到数据源  
  
1.  单击智能标记标志符号 (![智能标记标志符号](./media/vs-winformsmttagglyph.gif "VS_WinFormSmtTagGlyph")) 右上角的<xref:System.Windows.Forms.DataGridView>控件。  
  
2.  单击“选择数据源”选项的下拉箭头。  
  
3.  如果项目尚没有数据源，请单击“添加项目数据源”，按照向导指示的步骤进行操作。  
  
     有关详细信息，请参阅[数据源配置向导](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/w4dd7z6t(v=vs.120))。 新数据源将显示在“选择数据源”下拉窗口中。 如果新数据源只包含一个成员（例如单个数据库表），控件将自动绑定到该成员。 否则，请记住执行下一步。  
  
4.  如果尚未展开，则展开“其他数据源”和“项目数据源”节点，然后选择绑定控件的数据源。  
  
5.  如果您的数据源包含多个成员，例如，如果你已创建<xref:System.Data.DataSet?displayProperty=nameWithType>，其中包含多个表，展开数据源，然后选择要绑定到特定成员。  
  
6.  若要创建主/从关系，在**选择数据源**第二个下拉窗口<xref:System.Windows.Forms.DataGridView>控件中，展开<xref:System.Windows.Forms.BindingSource>父表中，创建的然后从列表中选择相关的子表所示。  
  
    > [!NOTE]
    >  如果项目已有数据源，还可以使用“数据源”窗口创建数据窗体。 有关详细信息，请参阅[数据源窗口](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/6ckyxa83(v=vs.120))。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.BindingSource>
- <xref:System.Windows.Forms.DataGridView.DataMember%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.DataSource%2A?displayProperty=nameWithType>
- [如何：连接到数据库中的数据](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/fxk9yw1t(v=vs.120))
- [如何：添加和使用设计器在 Windows 窗体 DataGridView 控件中删除列](add-and-remove-columns-in-the-datagrid-using-the-designer.md)
- [如何：更改使用设计器在 Windows 窗体 DataGridView 控件中的列顺序](change-the-order-of-columns-in-the-datagrid-using-the-designer.md)
- [如何：更改 Windows 窗体 DataGridView 列使用设计器的类型](change-the-type-of-a-wf-datagridview-column-using-the-designer.md)
- [如何：冻结使用设计器在 Windows 窗体 DataGridView 控件中的列](freeze-columns-in-the-datagrid-using-the-designer.md)
- [如何：在使用设计器在 Windows 窗体 DataGridView 控件中隐藏列](hide-columns-in-the-datagrid-using-the-designer.md)
- [如何：使列成为只读使用设计器在 Windows 窗体 DataGridView 控件中](make-columns-read-only-in-the-datagrid-using-the-designer.md)
- [如何：创建 Windows 窗体应用程序项目](/visualstudio/ide/step-1-create-a-windows-forms-application-project)
- [如何：向 Windows 窗体添加控件](how-to-add-controls-to-windows-forms.md)
- [数据源窗口](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/6ckyxa83(v=vs.120))
- [如何：在 Windows 窗体应用程序中显示相关的数据](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/57tx3hhe(v=vs.120))
