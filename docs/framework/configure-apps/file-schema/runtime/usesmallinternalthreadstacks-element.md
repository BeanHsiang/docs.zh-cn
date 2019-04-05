---
title: <UseSmallInternalThreadStacks> 元素
ms.date: 03/30/2017
helpviewer_keywords:
- UseSmallInternalThreadStacks element
- <UseSmallInternalThreadStacks> element
ms.assetid: 1e3f6ec0-1cac-4e1c-9c81-17d948ae5874
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d78d03956db3f50b4d01f06c9a6438afd62fac5d
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55289791"
---
# <a name="usesmallinternalthreadstacks-element"></a>\<UseSmallInternalThreadStacks > 元素
请求公共语言运行时 (CLR)，减少内存使用通过指定显式堆栈大小，当它创建的某些线程，它在内部使用，而不是使用这些线程的默认堆栈大小。  
  
 \<配置 > 元素  
\<运行时 > 元素  
\<UseSmallInternalThreadStacks > 元素  
  
## <a name="syntax"></a>语法  
  
```xml  
<UseSmallInternalThreadStacks enabled="true|false" />  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|enabled|必需的特性。<br /><br /> 指定是否要求，CLR 使用显式堆栈大小，而不是默认堆栈大小时创建的某些线程，它在内部使用。 显式堆栈大小都小于 1 MB 的默认堆栈大小。|  
  
## <a name="enabled-attribute"></a>enabled 特性  
  
|值|描述|  
|-----------|-----------------|  
|true|请求显式堆栈大小。|  
|False|使用默认堆栈大小。 这是默认[!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)]。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## <a name="remarks"></a>备注  
 此配置元素用于请求降低了的虚拟内存使用在进程中，因为 CLR 如果接受请求，对其内部线程，使用显式线程大小小于默认大小。  
  
> [!IMPORTANT]
>  此配置元素是对 CLR，而不是绝对要求的请求。 在[!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)]，则请求响应仅针对 x86 体系结构。 此元素可能会在 CLR 的未来版本中完全忽略或替换为显式堆栈大小始终用于所选的内部线程。  
  
 指定此配置元素交易的可靠性较小的虚拟内存使用 CLR 允许该请求，但是否因为较小的堆栈大小可能会使堆栈更有可能溢出。  
  
## <a name="example"></a>示例  
 下面的示例演示如何请求 CLR 使用显式堆栈调整某些大小在内部使用的线程。  
  
```xml  
<configuration>  
   <runtime>  
      <UseSmallInternalThreadStacks enabled="true" />  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅
- [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)
- [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)
