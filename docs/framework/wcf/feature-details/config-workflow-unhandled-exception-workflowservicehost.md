---
title: 如何：配置工作流未经处理的异常行为使用 WorkflowServiceHost
ms.date: 03/30/2017
ms.assetid: 51b25c86-292c-43e4-8d13-273d2badc8ad
ms.openlocfilehash: 9a13bb9390e891295491722898bd780bc1cac587
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54636152"
---
# <a name="how-to-configure-workflow-unhandled-exception-behavior-with-workflowservicehost"></a>如何：配置工作流未经处理的异常行为使用 WorkflowServiceHost
<xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior> 行为可用于指定 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 承载的工作流中出现未经处理的异常时所采取的操作。 本主题演示如何在配置文件中配置此行为。  
  
### <a name="to-configure-workflowunhandledexceptionbehavior"></a>配置 WorkflowUnhandledExceptionBehavior  
  
1.  添加 <`workflowUnhandledException`> 元素中的 <`behavior`> 元素中的 <`serviceBehaviors`> 元素中，使用`action`特性以指定要执行下面的示例中所示发生未处理的异常时的操作。  
  
    ```xml  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="">  
          <workflowUnhandledException action="abandonAndSuspend"/>   
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    ```  
  
    > [!NOTE]
    >  上面的配置示例使用的是简化配置。 有关详细信息，请参阅[Simplified Configuration](../../../../docs/framework/wcf/simplified-configuration.md)。  
  
     可在代码中配置该行为，如下面的示例所示。  
  
    ```csharp  
    host.Description.Behaviors.Add(new WorkflowUnhandledExceptionBehavior { Action = WorkflowUnhandledExceptionAction.AbandonAndSuspend });  
    ```  
  
     `action`属性的 <`workflowUnhandledException`> 元素可以设置为以下值之一：  
  
     **abandon**  
     中止内存中的实例，而不影响保存的实例状态（即回滚到上一个保存点）。  
  
     **abandonAndSuspend**  
     中止内存中的实例并将保存的实例更新为挂起。  
  
     **cancel**  
     为实例调用取消处理程序，然后在内存中完成该实例，此操作也有可能将实例从实例存储区中移除。  
  
     **terminate**  
     在内存中完成实例并将其从实例存储区中移除。  
  
     有关详细信息<xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior>，请参阅[Workflow Service Host Extensibility](../../../../docs/framework/wcf/feature-details/workflow-service-host-extensibility.md)。  
  
## <a name="see-also"></a>请参阅
- [工作流服务主机扩展性](../../../../docs/framework/wcf/feature-details/workflow-service-host-extensibility.md)
- [工作流服务](../../../../docs/framework/wcf/feature-details/workflow-services.md)
