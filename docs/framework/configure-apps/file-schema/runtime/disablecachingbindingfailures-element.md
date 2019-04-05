---
title: <disableCachingBindingFailures> 元素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#disableCachingBindingFailures
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/disableCachingBindingFailures
helpviewer_keywords:
- assemblies [.NET Framework],caching binding failures
- caching assembly binding failures
- <disableCachingBindingFailures> element
- disableCachingBindingFailures element
ms.assetid: bf598873-83b7-48de-8955-00b0504fbad0
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c99eb6b77a969a1c5003743b0407821e2537b683
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55289713"
---
# <a name="disablecachingbindingfailures-element"></a>\<disableCachingBindingFailures > 元素
指定是否禁用缓存绑定故障的原因是通过探测找不到程序集。  
  
 \<配置 > 元素  
\<运行时 > 元素  
\<disableCachingBindingFailures>  
  
## <a name="syntax"></a>语法  
  
```xml  
<disableCachingBindingFailures enabled="0|1"/>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|enabled|必需的特性。<br /><br /> 指定是否禁用缓存绑定故障的原因是通过探测找不到程序集。|  
  
## <a name="enabled-attribute"></a>enabled 特性  
  
|值|描述|  
|-----------|-----------------|  
|0|不要禁用绑定失败的原因是通过探测找不到程序集缓存。 这是从.NET Framework 2.0 版的默认绑定行为。|  
|1|禁用的绑定失败的原因是通过探测找不到程序集缓存。 此设置将恢复为.NET Framework 1.1 版的绑定行为。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## <a name="remarks"></a>备注  
 从.NET Framework 2.0 版开始，加载程序集的默认行为是缓存所有绑定和加载失败。 即，如果尝试加载程序集失败，后续请求同一程序集加载立即失败，而无需任何尝试查找程序集。 此元素将禁用绑定失败的原因是探测路径中找不到程序集的默认行为。 这些失败引发<xref:System.IO.FileNotFoundException>。  
  
 一些绑定和加载失败不受此元素，并始终进行缓存。 这些失败原因是该程序集已找到，但无法加载。 它们将引发<xref:System.BadImageFormatException>或<xref:System.IO.FileLoadException>。 以下列表包含此类故障的一些示例。  
  
-   如果你尝试加载文件不是有效的程序集，即使错误的文件将被替换为正确的程序集加载程序集的后续尝试将失败。  
  
-   如果尝试加载已锁定的文件系统程序集，加载程序集的后续尝试将失败，即使文件系统发布程序集。  
  
-   如果尝试加载的程序集的一个或多个版本位于探测路径中，但在它们之间的不是你请求的特定版本，加载该版本的后续尝试将失败，即使正确的版本将移到探测路径。  
  
## <a name="example"></a>示例  
 下面的示例演示如何禁用的原因是通过探测找不到程序集的程序集绑定故障缓存。  
  
```xml  
<configuration>  
   <runtime>  
      <disableCachingBindingFailures enabled="1" />  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅
- [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)
- [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)
- [运行时如何定位程序集](../../../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)
