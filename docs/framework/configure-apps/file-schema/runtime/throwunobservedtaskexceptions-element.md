---
title: <ThrowUnobservedTaskExceptions> 元素
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ThrowUnobservedTaskExceptions element
- <ThrowUnobservedTaskExceptions> element
ms.assetid: cea7e588-8b8d-48d2-9ad5-8feaf3642c18
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3bc2bffa11c3205c265ca21a9d4c4caa9b31d4e9
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55281497"
---
# <a name="throwunobservedtaskexceptions-element"></a>\<ThrowUnobservedTaskExceptions > 元素
指定未经处理的任务异常是否应终止正在运行的进程。  
  
 \<configuration>  
\<运行时 >  
\<ThrowUnobservedTaskExceptions>  
  
## <a name="syntax"></a>语法  
  
```xml  
<ThrowUnobservedTaskExceptions  
   enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`enabled`|必需的特性。<br /><br /> 指定未经处理的任务异常是否应终止正在运行的进程。|  
  
## <a name="enabled-attribute"></a>enabled 特性  
  
|值|描述|  
|-----------|-----------------|  
|`false`|不会终止正在运行的进程的未经处理的任务异常。 这是默认设置。|  
|`true`|终止正在运行的进程的未经处理的任务异常。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关运行时初始化选项的信息。|  
|||  
  
## <a name="remarks"></a>备注  
 如果与关联的异常<xref:System.Threading.Tasks.Task>未观察，没有任何<xref:System.Threading.Tasks.Task.Wait%2A>未附加操作，父级，和<xref:System.Threading.Tasks.Task.Exception%2A?displayProperty=nameWithType>属性未读取任务异常被视为未观察到。  
  
 在中[!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)]，也可由默认情况下，如果<xref:System.Threading.Tasks.Task>具有未观察到异常进行垃圾收集，终结器引发异常，并终止进程。 终止进程取决于垃圾回收和终止的时间。  
  
 为了简化开发人员能够编写基于任务的异步代码[!INCLUDE[net_v45](../../../../../includes/net-v45-md.md)]更改此默认行为为未观察到异常。 未观察到的异常仍会导致<xref:System.Threading.Tasks.TaskScheduler.UnobservedTaskException>事件被引发，但默认情况下，该过程不会终止。 相反，该异常被忽略后引发该事件，而不考虑是否将事件处理程序观察异常。  
  
 在中[!INCLUDE[net_v45](../../../../../includes/net-v45-md.md)]，可以使用[ \<ThrowUnobservedTaskExceptions > 元素](../../../../../docs/framework/configure-apps/file-schema/runtime/throwunobservedtaskexceptions-element.md)若要启用应用程序配置文件中[!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)]引发异常的行为。  
  
 此外可以通过以下方式之一中指定的异常行为：  
  
-   通过设置环境变量`COMPlus_ThrowUnobservedTaskExceptions`(`set COMPlus_ThrowUnobservedTaskExceptions=1`)。  
  
-   通过设置注册表 DWORD 值 ThrowUnobservedTaskExceptions = 1 在 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\。NETFramework 键。  
  
## <a name="example"></a>示例  
 下面的示例演示如何启用任务中的异常引发使用应用程序配置文件。  
  
```xml  
<configuration>   
    <runtime>   
        <ThrowUnobservedTaskExceptions enabled="true"/>   
    </runtime>   
</configuration>  
```  
  
## <a name="example"></a>示例  
 下面的示例演示如何从任务引发未观察到的异常。 作为已发布的程序才能正常工作，必须运行代码。  
  
 [!code-csharp[ThrowUnobservedTaskExceptions#1](../../../../../samples/snippets/csharp/VS_Snippets_CLR/throwunobservedtaskexceptions/cs/program.cs#1)]
 [!code-vb[ThrowUnobservedTaskExceptions#1](../../../../../samples/snippets/visualbasic/VS_Snippets_CLR/throwunobservedtaskexceptions/vb/program.vb#1)]  
  
## <a name="see-also"></a>请参阅
- [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)
- [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)
