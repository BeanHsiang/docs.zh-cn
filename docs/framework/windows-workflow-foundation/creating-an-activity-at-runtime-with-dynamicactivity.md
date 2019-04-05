---
title: 使用 DynamicActivity 在运行时创建活动
ms.date: 03/30/2017
ms.assetid: 1af85cc6-912d-449e-90c5-c5db3eca5ace
ms.openlocfilehash: 58dea5f6e469f871da35fc57aa4d9d8a1266bfed
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57724614"
---
# <a name="creating-an-activity-at-runtime-with-dynamicactivity"></a>使用 DynamicActivity 在运行时创建活动
<xref:System.Activities.DynamicActivity> 是一个带有公共构造函数的具体的密封类。 通过使用活动 DOM，<xref:System.Activities.DynamicActivity> 可用于在运行时组合活动功能。  
  
## <a name="dynamicactivity-features"></a>DynamicActivity 功能  
 <xref:System.Activities.DynamicActivity> 有权访问执行属性、参数和变量，但无权访问运行时服务（例如安排子活动或跟踪）。  
  
 使用工作流 <xref:System.Activities.Argument> 对象可以设置顶级属性。 在命令性代码中，使用新类型的 CLR 属性创建这些参数。 在 XAML 中，使用 `x:Class` 和 `x:Member` 标记声明这些参数。  
  
 使用 <xref:System.Activities.DynamicActivity> 构造的活动使用 <xref:System.ComponentModel.ICustomTypeDescriptor> 与设计器交互。 可以使用 <xref:System.Activities.XamlIntegration.ActivityXamlServices.Load%2A> 动态加载在设计器中创建的活动，如下面的过程所示。  
  
#### <a name="to-create-an-activity-at-runtime-using-imperative-code"></a>使用命令性代码在运行时创建活动  
  
1.  OpenVisual Studio 2010.  
  
2.  选择**文件**，**新**，**项目**。 选择**Workflow 4.0**下**Visual C#** 中**项目类型**窗口中，然后选择**v2010**节点。 选择**顺序工作流控制台应用程序**中**模板**窗口。 将新项目命名为 DynamicActivitySample。  
  
3.  在 HelloActivity 项目中右击 Workflow1.xaml，然后选择**删除**。  
  
4.  打开 Program.cs。 将下面的指令添加到文件的顶部。  
  
    ```  
    using System.Collections.Generic;  
    ```  
  
5.  将 `Main` 方法的内容替换为以下代码，这会创建一个包含单个 <xref:System.Activities.Statements.Sequence> 活动的 <xref:System.Activities.Statements.WriteLine> 活动，并将后者赋给新动态活动的 <xref:System.Activities.DynamicActivity.Implementation%2A> 属性。  
  
    ```csharp  
    //Define the input argument for the activity  
    var textOut = new InArgument<string>();  
    //Create the activity, property, and implementation  
                Activity dynamicWorkflow = new DynamicActivity()  
                {  
                    Properties =   
                    {  
                        new DynamicActivityProperty  
                        {  
                            Name = "Text",  
                            Type = typeof(InArgument<String>),  
                            Value = textOut  
                        }  
                    },  
                    Implementation = () => new Sequence()  
                    {  
                        Activities =   
                        {  
                            new WriteLine()  
                            {  
                                Text = new InArgument<string>(env => textOut.Get(env))  
                            }  
                        }  
                    }  
                };  
    //Execute the activity with a parameter dictionary  
                WorkflowInvoker.Invoke(dynamicWorkflow, new Dictionary<string, object> { { "Text", "Hello World!" } });  
                Console.ReadLine();  
    ```  
  
6.  执行应用程序。 具有文本"Hello World ！"的控制台窗口 显示。  
  
#### <a name="to-create-an-activity-at-runtime-using-xaml"></a>使用 XAML 在运行时创建活动  
  
1.  打开 Visual Studio 2010。  
  
2.  选择**文件**，**新**，**项目**。 选择**Workflow 4.0**下**Visual C#** 中**项目类型**窗口中，然后选择**v2010**节点。 选择**工作流控制台应用程序**中**模板**窗口。 将新项目命名为 DynamicActivitySample。  
  
3.  在 HelloActivity 项目中打开 Workflow1.xaml。 单击**自变量**设计器底部的选项。 创建一个 `In` 类型的新 `TextToWrite` 自变量，并将其命名为 `String`。  
  
4.  拖动**WriteLine**活动从**基元**部分中的工具箱拖到设计器图面。 将该值赋`TextToWrite`到**文本**活动属性。  
  
5.  打开 Program.cs。 将下面的指令添加到文件的顶部。  
  
    ```  
    using System.Activities.XamlIntegration;  
    ```  
  
6.  将 `Main` 方法的内容替换为以下代码。  
  
    ```  
    Activity act2 = ActivityXamlServices.Load(@"Workflow1.xaml");  
                    results = WorkflowInvoker.Invoke(act2, new Dictionary<string, object> { { "TextToWrite", "HelloWorld!" } });  
    Console.ReadLine();  
    ```  
  
7.  执行应用程序。 具有文本"Hello World ！"的控制台窗口 将出现。  
  
8.  右击 Workflow1.xaml 文件中的**解决方案资源管理器**，然后选择**查看代码**。 请注意，活动类使用 `x:Class` 创建，属性使用 `x:Property` 创建。  
  
## <a name="see-also"></a>请参阅

- [使用强制性代码创建工作流、活动和表达式](authoring-workflows-activities-and-expressions-using-imperative-code.md)
