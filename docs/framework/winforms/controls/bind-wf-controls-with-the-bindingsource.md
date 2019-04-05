---
title: 如何：将 Windows 窗体控件与 BindingSource 组件使用设计器绑定
ms.date: 03/30/2017
helpviewer_keywords:
- controls [Windows Forms], binding
- BindingSource component [Windows Forms], binding controls
- data binding [Windows Forms], BindingSource component
ms.assetid: 391ae170-de5c-40f8-8233-91cb2ee4683a
ms.openlocfilehash: e12498bc71957d49893e49e54095b6bb184ac2c3
ms.sourcegitcommit: acd8ed14fe94e9d4e3a7fb685fe83d05e941073c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2019
ms.locfileid: "56441913"
---
# <a name="how-to-bind-windows-forms-controls-with-the-bindingsource-component-using-the-designer"></a>如何：将 Windows 窗体控件与 BindingSource 组件使用设计器绑定
在已向窗体添加控件并为你的应用程序确定的用户界面后，可以将控件绑定到数据源，以便在运行时，用户可以更改和保存到应用程序相关的数据。  
  
 在 Windows 窗体中绑定的控件的一系列使用非常轻松地实现<xref:System.Windows.Forms.BindingSource>控件作为窗体上的控件和数据源之间的桥梁。  
  
 在窗体上的一个或多个控件可以绑定到数据;在下面的过程，<xref:System.Windows.Forms.TextBox>控件绑定到数据源。  
  
 若要完成该过程，假定您将绑定到派生自数据库的数据源。 从其他存储的数据创建数据源的详细信息，请参阅[添加新数据源](/visualstudio/data-tools/add-new-data-sources)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
### <a name="to-bind-a-control-at-design-time"></a>若要将控件绑定在设计时  
  
1.  拖动<xref:System.Windows.Forms.TextBox>到窗体控件。  
  
2.  在中**属性**窗口：  
  
    1.  展开 **(DataBindings)** 节点。  
  
    2.  单击箭头旁边<xref:System.Windows.Forms.TextBox.Text%2A>属性。  
  
         **数据源**UI 类型编辑器将打开。  
  
         如果以前已为项目或窗体配置数据源，它将出现。  
  
3.  单击“添加项目数据源”以连接到数据并创建一个数据源。  
  
4.  在“数据源配置向导”欢迎页上，单击“下一步”。  
  
5.  上**选择数据源类型**页上，选择**数据库**。  
  
6.  上**选择数据连接**页上，从可用连接列表中选择一个数据连接。 如果所需的数据连接不可用，请选择**新的连接**若要创建新的数据连接。  
  
7.  选择**是，将连接保存**应用程序配置文件中保存连接字符串。  
  
8.  选择要放置到应用程序中的数据库对象。 在这种情况下，选择你想的表中的一个字段<xref:System.Windows.Forms.TextBox>显示。  
  
9. 如果愿意，可以替换默认的数据集名称。  
  
10. 单击 **“完成”**。  
  
11. 在中**属性**窗口中，单击旁边的箭头<xref:System.Windows.Forms.TextBox.Text%2A>试属性。 在中**数据源**UI 类型编辑器中，选择要绑定的字段名称<xref:System.Windows.Forms.TextBox>到。  
  
     **数据源**UI 类型编辑器将关闭并且数据集，<xref:System.Windows.Forms.BindingSource>和特定于数据连接添加到你的窗体的表适配器。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.BindingSource>
- <xref:System.Windows.Forms.BindingNavigator>
- [添加新数据源](/visualstudio/data-tools/add-new-data-sources)
- [数据源窗口](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/6ckyxa83(v=vs.120))