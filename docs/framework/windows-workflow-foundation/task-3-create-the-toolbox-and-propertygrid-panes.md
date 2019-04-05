---
title: 任务 3:创建工具箱和属性网格窗格
ms.date: 03/30/2017
ms.assetid: 72c1546a-eed5-4f0f-a616-719a163414f4
ms.openlocfilehash: 45819577c39185a5d95da81521cd541087a64efc
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57721212"
---
# <a name="task-3-create-the-toolbox-and-propertygrid-panes"></a>任务 3:创建工具箱和属性网格窗格
在本任务中，您将创建**工具箱**并**PropertyGrid**窗格并将其添加到重新承载[!INCLUDE[wfd1](../../../includes/wfd1-md.md)]。  
  
 有关参考中的任务应在完成这三个后 MainWindow.xaml.cs 文件中的代码[重新承载工作流设计器](rehosting-the-workflow-designer.md)系列主题提供本主题末尾处。  
  
### <a name="to-create-the-toolbox-and-add-it-to-the-grid"></a>创建工具箱并将其添加到网格中  
  
1.  打开按照中所述的过程获得的 HostingApplication 项目[任务 2:承载工作流设计器](task-2-host-the-workflow-designer.md)。  
  
2.  在中**解决方案资源管理器**窗格中，右击 MainWindow.xaml 文件，并选择**查看代码**。  
  
3.  添加`GetToolboxControl`方法`MainWindow`类，该类创建<xref:System.Activities.Presentation.Toolbox.ToolboxControl>，添加一个新**工具箱**类别与**工具箱**，并将分配<xref:System.Activities.Statements.Assign>和<xref:System.Activities.Statements.Sequence>向该类别的活动类型。  
  
    ```csharp  
    private ToolboxControl GetToolboxControl()  
    {  
        // Create the ToolBoxControl.  
        ToolboxControl ctrl = new ToolboxControl();  
  
        // Create a category.  
        ToolboxCategory category = new ToolboxCategory("category1");  
  
        // Create Toolbox items.  
        ToolboxItemWrapper tool1 =   
            new ToolboxItemWrapper("System.Activities.Statements.Assign",   
            typeof(Assign).Assembly.FullName, null, "Assign");  
  
        ToolboxItemWrapper tool2 = new ToolboxItemWrapper("System.Activities.Statements.Sequence",   
            typeof(Sequence).Assembly.FullName, null, "Sequence");  
  
        // Add the Toolbox items to the category.  
        category.Add(tool1);  
        category.Add(tool2);  
  
        // Add the category to the ToolBox control.  
        ctrl.Categories.Add(category);  
        return ctrl;  
    }  
    ```  
  
4.  添加一个私有`AddToolbox`方法`MainWindow`类将放置**工具箱**网格上的左侧列中。  
  
    ```csharp  
    private void AddToolBox()  
    {  
        ToolboxControl tc = GetToolboxControl();  
        Grid.SetColumn(tc, 0);  
        grid1.Children.Add(tc);  
    }  
    ```  
  
5.  在 `AddToolBox` 类构造函数中添加对 `MainWindow()` 方法的调用，如以下代码所示。  
  
    ```csharp  
    public MainWindow()  
    {  
        InitializeComponent();  
        this.RegisterMetadata();  
        this.AddDesigner();  
  
        this.AddToolBox();  
    }  
    ```  
  
6.  按“F5”生成并运行解决方案。 **工具箱**包含<xref:System.Activities.Statements.Assign>和<xref:System.Activities.Statements.Sequence>应显示的活动。  
  
### <a name="to-create-the-propertygrid"></a>创建属性网格  
  
1.  在中**解决方案资源管理器**窗格中，右击 MainWindow.xaml 文件，并选择**查看代码**。  
  
2.  添加`AddPropertyInspector`方法`MainWindow`类，以放置**PropertyGrid**网格上的最右侧列中的窗格。  
  
    ```csharp  
    private void AddPropertyInspector()  
    {  
        Grid.SetColumn(wd.PropertyInspectorView, 2);  
        grid1.Children.Add(wd.PropertyInspectorView);              
    }  
    ```  
  
3.  在 `AddPropertyInspector` 类构造函数中添加对 `MainWindow()` 方法的调用，如以下代码所示。  
  
    ```csharp  
    public MainWindow()  
    {  
        InitializeComponent();  
        this.RegisterMetadata();  
        this.AddDesigner();  
        this.AddToolBox();  
  
        this.AddPropertyInspector();   
    }  
    ```  
  
4.  按 F5 生成并运行解决方案。 **工具箱**，工作流设计画布和**PropertyGrid**窗格应显示，并拖动时<xref:System.Activities.Statements.Assign>活动或<xref:System.Activities.Statements.Sequence>到设计画布上的活动属性网格应根据突出显示的活动更新。  
  
## <a name="example"></a>示例  
 现在，MainWindow.xaml.cs 文件应包含以下代码。  
  
```  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.Windows;  
using System.Windows.Controls;  
using System.Windows.Data;  
using System.Windows.Documents;  
using System.Windows.Input;  
using System.Windows.Media;  
using System.Windows.Media.Imaging;  
using System.Windows.Navigation;  
using System.Windows.Shapes;  
//dlls added  
using System.Activities;  
using System.Activities.Core.Presentation;  
using System.Activities.Presentation;  
using System.Activities.Presentation.Metadata;  
using System.Activities.Presentation.Toolbox;  
using System.Activities.Statements;  
using System.ComponentModel;  
  
namespace HostingApplication  
{  
    /// <summary>  
    /// Interaction logic for MainWindow.xaml  
    /// </summary>  
    public partial class MainWindow : Window  
    {  
        private WorkflowDesigner wd;  
  
        public MainWindow()  
        {  
            InitializeComponent();  
            RegisterMetadata();  
            AddDesigner();  
            this.AddToolBox();  
            this.AddPropertyInspector();  
        }  
  
        private void AddDesigner()  
        {  
            //Create an instance of WorkflowDesigner class.  
            this.wd = new WorkflowDesigner();  
  
            //Place the designer canvas in the middle column of the grid.  
            Grid.SetColumn(this.wd.View, 1);  
  
            //Load a new Sequence as default.  
            this.wd.Load(new Sequence());  
  
            //Add the designer canvas to the grid.  
            grid1.Children.Add(this.wd.View);  
        }  
  
        private void RegisterMetadata()  
        {  
            DesignerMetadata dm = new DesignerMetadata();  
            dm.Register();  
        }  
  
        private ToolboxControl GetToolboxControl()  
        {  
            // Create the ToolBoxControl.  
            ToolboxControl ctrl = new ToolboxControl();  
  
            // Create a category.  
            ToolboxCategory category = new ToolboxCategory("category1");  
  
            // Create Toolbox items.  
            ToolboxItemWrapper tool1 =  
                new ToolboxItemWrapper("System.Activities.Statements.Assign",  
                typeof(Assign).Assembly.FullName, null, "Assign");  
  
            ToolboxItemWrapper tool2 = new ToolboxItemWrapper("System.Activities.Statements.Sequence",  
                typeof(Sequence).Assembly.FullName, null, "Sequence");  
  
            // Add the Toolbox items to the category.  
            category.Add(tool1);  
            category.Add(tool2);  
  
            // Add the category to the ToolBox control.  
            ctrl.Categories.Add(category);  
            return ctrl;  
        }  
  
        private void AddToolBox()  
        {  
            ToolboxControl tc = GetToolboxControl();  
            Grid.SetColumn(tc, 0);  
            grid1.Children.Add(tc);  
        }  
  
        private void AddPropertyInspector()  
        {  
            Grid.SetColumn(wd.PropertyInspectorView, 2);  
            grid1.Children.Add(wd.PropertyInspectorView);  
        }  
  
    }  
}  
```  
  
## <a name="see-also"></a>请参阅
- [重新托管工作流设计器](rehosting-the-workflow-designer.md)
- [任务 1:创建新的 Windows Presentation Foundation 应用程序](task-1-create-a-new-wpf-app.md)
- [任务 2:承载工作流设计器](task-2-host-the-workflow-designer.md)
