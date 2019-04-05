---
title: <add> 的 <commonParameters>
ms.date: 03/30/2017
ms.assetid: 3713bf25-20c8-455f-bb85-de46b6487932
ms.openlocfilehash: e0ca00911577f9f210def9326df261f772f9c26d
ms.sourcegitcommit: b8ace47d839f943f785b89e2fff8092b0bf8f565
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2019
ms.locfileid: "55674420"
---
# <a name="add-of-commonparameters"></a>\<add> of \<commonParameters>
指定在多个服务之间全局使用的参数的名称/值对。 此参数通常包括可由持久性服务共享的数据库连接字符串。  
  
 \<system.ServiceModel>  
\<behaviors>  
\<serviceBehaviors>  
\<behavior>  
\<workflowRuntime>  
\<commonParameters>  
\<add>  
  
## <a name="syntax"></a>语法  
  
```xml  
<workflowRuntime>
  <commonParameters>
    <add name="String" value="String" />
  </commonParameters>
</workflowRuntime>
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|name|为服务指定的参数的名称。|  
|值|为服务指定的参数的值。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<commonParameters>](commonparameters.md)|服务使用的公用参数的集合。 此集合通常将包括可由持久性服务共享的数据库连接字符串。|  
  
## <a name="remarks"></a>备注  
 `<commonParameters>` 元素定义在多个服务之间全局使用的任何参数，例如，使用 `ConnectionString` 时的<xref:System.Workflow.Runtime.Hosting.SharedConnectionWorkflowCommitWorkBatchService>。  
  
 对于提交批处理工作进行永久性存储的服务，如 <xref:System.Workflow.Runtime.Hosting.DefaultWorkflowCommitWorkBatchService> 和 <xref:System.Workflow.Runtime.Hosting.SqlWorkflowPersistenceService>，可以通过使用 `EnableRetries` 参数来允许它们重试其事务，如以下示例所示：  
  
```xml  
<workflowRuntime name="SampleApplication"
                 unloadOnIdle="false">
  <commonParameters>
    <add name="ConnectionString"
         value="Initial Catalog=WorkflowStore;Data Source=localhost;Integrated Security=SSPI;" />
    <add name="EnableRetries"
         value="True" />
  </commonParameters>
  <services>
    <add type="System.Workflow.Runtime.Hosting.SqlWorkflowPersistenceService, System.Workflow.Runtime, Version=3.0.00000.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35"
         enableRetries="False" />
  </services>
</workflowRuntime>
```  
  
 请注意，`EnableRetries`参数可设置为在全局级别 (如中所示*CommonParameters*部分) 或为个别支持的服务`EnableRetries`(如中所示*服务*部分)。  
  
 有关使用配置文件来控制行为的详细信息<xref:System.Workflow.Runtime.WorkflowRuntime>对象的 Windows Workflow Foundation 主机应用程序，请参阅[工作流配置文件](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms732240(v=vs.90))。  
  
## <a name="example"></a>示例  
  
```xml  
<commonParameters>
  <add name="ConnectionString"
       value="Initial Catalog=WorkflowStore;Data Source=localhost;Integrated Security=SSPI;" />
  <add name="EnableRetries"
       value="true" />
</commonParameters>
```  
  
## <a name="see-also"></a>请参阅
- <xref:System.ServiceModel.Configuration.WorkflowRuntimeElement>
- <xref:System.Workflow.Runtime.Configuration.WorkflowRuntimeServiceElement>
- <xref:System.Workflow.Runtime.WorkflowRuntime>
- <xref:System.Workflow.Runtime.Hosting.DefaultWorkflowCommitWorkBatchService>
- <xref:System.Workflow.Runtime.Hosting.SqlWorkflowPersistenceService>
- [工作流配置文件](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms732240(v=vs.90))
- [\<commonParameters>](commonparameters.md)
