---
title: 如何：创建自定义活动模板
ms.date: 03/30/2017
ms.assetid: 6760a5cc-6eb8-465f-b4fa-f89b39539429
ms.openlocfilehash: f9594f799e1b6a176e7bbf28cdea77c9cdfb70ac
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57703460"
---
# <a name="how-to-create-a-custom-activity-template"></a>如何：创建自定义活动模板

可使用自定义活动模板来自定义活动（包括自定义复合活动）的配置，使用户无需单独创建每个活动并手动配置其属性和其他设置。 这些自定义模板可用于在**工具箱**上[!INCLUDE[wfd1](../../../includes/wfd1-md.md)]或从重新承载设计器，从该用户可以将它们拖到预配置的设计图面。 [!INCLUDE[wfd2](../../../includes/wfd2-md.md)] 附带了此类模板的很好的示例： [SendAndReceiveReply 模板设计器](/visualstudio/workflow-designer/sendandreceivereply-template-designer)并[ReceiveAndSendReply 模板设计器](/visualstudio/workflow-designer/receiveandsendreply-template-designer)中[消息传递活动设计器](/visualstudio/workflow-designer/messaging-activity-designers)类别。

 本主题中的第一个过程介绍如何创建自定义活动模板**延迟**活动和第二个过程简要描述如何使其可在[!INCLUDE[wfd2](../../../includes/wfd2-md.md)]若要验证的自定义模板是否正常工作。

 自定义活动模板必须实现 <xref:System.Activities.Presentation.IActivityTemplateFactory>。 此接口具有一个 <xref:System.Activities.Presentation.IActivityTemplateFactory.Create%2A> 方法，可利用此方法创建和配置模板中使用的活动实例。

## <a name="to-create-a-template-for-the-delay-activity"></a>为 Delay 活动创建模板

1.  启动 Visual Studio 2010。

2.  在“文件”菜单上，指向“新建”，然后选择“项目”。

     **“新建项目”** 对话框随即打开。

3.  在中**项目类型**窗格中，选择**工作流**眖**Visual C#** 项目或**Visual Basic**分组，具体取决于你语言首选项。

4.  在中**模板**窗格中，选择**活动库**。

5.  在中**名称**框中，输入`DelayActivityTemplate`。

6.  接受中的默认值**位置**并**解决方案名称**文本框中，并单击**确定**。

7.  右击 DelayActivityTemplate 项目中引用目录**解决方案资源管理器**，然后选择**添加引用**以打开**添加引用**对话框。

8.  转到 **.NET**选项卡并选择**PresentationFramework**从**组件名称**列在左侧和单击**确定**添加的引用对 PresentationFramework.dll 文件中。

9. 重复此过程以添加对 System.Activities.Presentation.dll 文件和 WindowsBase.dll 文件的引用。

10. 右击 DelayActivityTemplate 项目中的**解决方案资源管理器**，然后选择**添加**，然后**新项**以打开**添加新项**对话框。

11. 选择**类**模板，其命名为 MyDelayTemplate，然后依次**确定**。

12. 打开 MyDelayTemplate.cs 文件并添加下面的语句。

    ```
    //Namespaces added
    using System.Activities;
    using System.Activities.Statements;
    using System.Activities.Presentation;
    using System.Windows;
    ```

13. 使用带有以下代码的 <xref:System.Activities.Presentation.IActivityTemplateFactory> 类来实现 `MyDelayActivity`。 这会将延迟时间配置为 10 秒。

    ```
    public sealed class MyDelayActivity : IActivityTemplateFactory
    {
        public Activity Create(System.Windows.DependencyObject target)
        {
            return new System.Activities.Statements.Delay
            {
                DisplayName = "DelayActivityTemplate",
                Duration = new TimeSpan(0, 0, 10)

            };
        }
    }
    ```

14. 选择**生成解决方案**从**生成**菜单以生成 DelayActivityTemplate.dll 文件。

### <a name="to-make-the-template-available-in-a-workflow-designer"></a>使模板在工作流设计器中可用

1.  右击 DelayActivityTemplate 解决方案中的**解决方案资源管理器**，然后选择**添加**，然后**新项目**以打开**添加新项目**对话框。

2.  选择**工作流控制台应用程序**模板，其命名`CustomActivityTemplateApp`，然后单击**确定**。

3.  右击 CustomActivityTemplateApp 项目中引用目录**解决方案资源管理器**，然后选择**添加引用**以打开**添加引用**对话框框。

4.  转到**项目**选项卡并选择**DelayActivityTemplate**从**项目名称**列在左侧和单击**确定**添加引用在第一个过程中创建的 DelayActivityTemplate.dll 文件。

5.  右击 CustomActivityTemplateApp 项目中的**解决方案资源管理器**，然后选择**生成**编译该应用程序。

6.  右击 CustomActivityTemplateApp 项目中的**解决方案资源管理器**，然后选择**设为启动项目**。

7.  选择**启动但不调试**从**调试**菜单并按任意键以继续在 cmd.exe 窗口中出现提示时。

8.  打开 Workflow1.xaml 文件，并打开**工具箱**。

9. 找到**MyDelayActivity**中的模板**DelayActivityTemplate**类别。 将此模板拖动到设计图面上。 在确认**属性**窗口的`Duration`属性设置为 10 秒。

## <a name="example"></a>示例
 MyDelayActivity.cs 文件应包含以下代码。

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

//Namespaces added
using System.Activities;
using System.Activities.Statements;
using System.Activities.Presentation;
using System.Windows;

namespace DelayActivityTemplate
{
    public sealed class MyDelayActivity : IActivityTemplateFactory
    {
        public Activity Create(System.Windows.DependencyObject target)
        {
            return new System.Activities.Statements.Delay
            {
                DisplayName = "DelayActivityTemplate",
                Duration = new TimeSpan(0, 0, 10)

            };
        }
    }
}
```

## <a name="see-also"></a>请参阅

- <xref:System.Activities.Presentation.IActivityTemplateFactory>
- [自定义工作流设计体验](customizing-the-workflow-design-experience.md)