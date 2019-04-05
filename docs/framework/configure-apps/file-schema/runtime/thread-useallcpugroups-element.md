---
title: < Thread_UseAllCpuGroups > 元素
ms.date: 03/30/2017
ms.assetid: d30fe7c5-8469-46e2-b804-e3eec7b24256
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 95411f5adde07c0d00124b2793b495c7ed8f49ef
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55288933"
---
# <a name="threaduseallcpugroups-element"></a>\<Thread_UseAllCpuGroups > 元素
指定运行时是否跨所有 CPU 组分发托管的线程。  
  
 \<configuration>  
\<运行时 >  
<Thread_UseAllCpuGroups>  
  
## <a name="syntax"></a>语法  
  
```xml
<Thread_UseAllCpuGroups    
   enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`enabled`|必需的特性。<br /><br /> 指定运行时是否跨所有 CPU 组分发托管的线程。|  
  
## <a name="enabled-attribute"></a>enabled 特性  
  
|值|描述|  
|-----------|-----------------|  
|`false`|在运行时不会跨多个 CPU 组分发托管的线程。 这是默认设置。|  
|`true`|在运行时将托管的线程分布到多个 CPU 组，如果计算机有多个 CPU 组和[ \<GCCpuGroup >](../../../../../docs/framework/configure-apps/file-schema/runtime/gccpugroup-element.md)启用元素。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## <a name="remarks"></a>备注  
 当一台计算机具有多个 CPU 组时，启用此元素会导致运行时的所有 CPU 组分发托管的线程。 若要使用此功能，还必须启用[ \<GCCpuGroup >](../../../../../docs/framework/configure-apps/file-schema/runtime/gccpugroup-element.md)元素，该扩展到所有 CPU 组的垃圾回收并将考虑在内时创建和平衡堆的所有核心元素。 启用[ \<GCCpuGroup >](../../../../../docs/framework/configure-apps/file-schema/runtime/gccpugroup-element.md)元素需要启用[ \<gcServer >](../../../../../docs/framework/configure-apps/file-schema/runtime/gcserver-element.md)元素。 如果未启用这些元素，则启用`<Thread_UseAllCpuGroups>`元素不起作用。  
  
## <a name="example"></a>示例  
 下面的示例演示如何启用对多个 CPU 组的支持。  
  
```xml  
<configuration>  
   <runtime>  
      <Thread_UseAllCpuGroups enabled="true"/>  
      <GCCpuGroup enabled="true"/>  
      <gcServer enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅
- [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)
- [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)
- [\<GCCpuGroup > 元素](../../../../../docs/framework/configure-apps/file-schema/runtime/gccpugroup-element.md)
