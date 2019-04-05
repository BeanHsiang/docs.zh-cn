---
title: 任务 1:创建新的 Windows Presentation Foundation 应用程序
ms.date: 03/30/2017
ms.assetid: 270eaeba-9492-4532-af9f-403ce5c9935b
ms.openlocfilehash: 533b4a1030ab5f47eb96ca62dc2805eae7933b9b
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57711878"
---
# <a name="task-1-create-a-new-windows-presentation-foundation-application"></a>任务 1:创建新的 Windows Presentation Foundation 应用程序
在此任务中，将使用 WPF 应用程序 Visual Studio 模板创建一个空的 Windows Presentation Foundation (WPF) 应用程序并将引用添加到相应[!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)]工作流程序集。  
  
### <a name="to-create-the-wpf-application-project"></a>创建 WPF 应用程序项目  
  
1.  打开 Visual Studio 并在**文件**菜单，依次指向**新建**，然后单击**项目**。  
  
2.  在中**新的项目**对话框框中，选择**Visual C#** 或**Visual Basic**从**已安装的模板**在左侧窗格一侧的框。 如果没有显示所选的语言下, 查找**其他语言**。  
  
3.  选择**Windows**中**已安装的模板**窗格。  
  
4.  在顶部窗格中，确认 （默认值） **.NET Framework 4**已被选择的下拉列表框中，并选择**WPF 应用程序**。  
  
5.  设置到项目的名称**HostingApplication**在窗口的底部。  
  
6.  将解决方案名称设置为**RehostingTheDesigner**。  
  
7.  单击**确定**创建应用程序项目。 Visual Studio 创建应用程序的一个基本 WPF UI，并包括相应的 XAML 和代码隐藏文件。  
  
8.  将引用添加到**WorkflowModel**程序集。 若要执行此操作，在**解决方案资源管理器**，右键单击**HostingApplication**项目，然后选择**添加引用**。  
  
9. 在中**添加引用**对话框中，单击 **.NET**选项卡上，请按住 CTRL 键，选择以下程序集，然后单击**确定**:  
  
    -   System.Activities  
  
    -   System.Activities.Presentation  
  
    -   System.Activities.Core.Presentation  
  
10. 单击 **“确定”**。  
  
11. 请参阅[任务 2:承载工作流设计器](task-2-host-the-workflow-designer.md)若要了解如何承载工作流设计器设计画布。  
  
## <a name="see-also"></a>请参阅
- [重新托管工作流设计器](rehosting-the-workflow-designer.md)
- [任务 2:承载工作流设计器](task-2-host-the-workflow-designer.md)
