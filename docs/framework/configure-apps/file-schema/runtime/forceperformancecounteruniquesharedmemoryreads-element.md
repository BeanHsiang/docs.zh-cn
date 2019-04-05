---
title: <forcePerformanceCounterUniqueSharedMemoryReads> 元素
ms.date: 03/30/2017
helpviewer_keywords:
- forcePerformanceCounterUniqueSharedMemoryReads element
- <forcePerformanceCounterUniqueSharedMemoryReads> element
ms.assetid: 91149858-4810-4f65-9b48-468488172c9b
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2ba70e7cc94f90fa4fd44a12ffb6ffb2dba1ccc7
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55275894"
---
# <a name="forceperformancecounteruniquesharedmemoryreads-element"></a>\<forcePerformanceCounterUniqueSharedMemoryReads > 元素
指定 PerfCounter.dll 是否使用 .NET Framework 版本 1.1 应用程序中的 CategoryOptions 注册表设置，以确定是否加载来自特定于类别的共享内存或全局内存的性能计数器数据。  
  
 \<configuration>  
\<运行时 >  
\<forcePerformanceCounterUniqueSharedMemoryReads>  
  
## <a name="syntax"></a>语法  
  
```xml  
<forcePerformanceCounterUniqueSharedMemoryReads   
enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`enabled`|必需的特性。<br /><br /> 指示 PerfCounter.dll 是否使用 CategoryOptions 注册表设置来确定是否要从特定于类别的共享的内存或全局内存加载性能计数器数据。|  
  
## <a name="enabled-attribute"></a>enabled 特性  
  
|值|描述|  
|-----------|-----------------|  
|`false`|PerfCounter.dll 不使用 CategoryOptions 注册表设置这是默认值。|  
|`true`|PerfCounter.dll 确实使用的 CategoryOptions 注册表设置。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## <a name="remarks"></a>备注  
 在之前的.NET framework 版本[!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)]，PerfCounter.dll 加载的版本对应于进程中加载的运行时。 如果计算机有两个.NET Framework 1.1 版和[!INCLUDE[dnprdnlong](../../../../../includes/dnprdnlong-md.md)]安装，.NET Framework 1.1 应用程序将加载 PerfCounter.dll 的.NET Framework 1.1 版本。 从开始[!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)]，加载最新安装的 PerfCounter.dll 版本。 这意味着.NET Framework 1.1 应用程序将加载[!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)]PerfCounter.dll 版本如果[!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)]的计算机上安装。  
  
 从开始[!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)]，PerfCounter.dll 时使用性能计数器，检查每个提供程序，以确定是否应从特定于类别的共享的内存或全局共享的内存读取的 CategoryOptions 注册表项。 .NET Framework 1.1 PerfCounter.dll 不读取该注册表项，因为它没有感知的特定于类别的共享内存;它始终从全局共享内存读取。  
  
 为了向后兼容， [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] PerfCounter.dll 在.NET Framework 1.1 应用程序中运行时不检查 CategoryOptions 注册表项。 它只需使用全局共享的内存，就像.NET Framework 1.1 PerfCounter.dll 一样。 但是，您可以指示[!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)]PerfCounter.dll 若要检查的注册表设置，从而`<forcePerformanceCounterUniqueSharedMemoryReads>`元素。  
  
> [!NOTE]
>  启用`<forcePerformanceCounterUniqueSharedMemoryReads>`元素不能保证将使用特定于类别的共享的内存。 启用到设置`true`仅会导致 PerfCounter.dll 要引用的 CategoryOptions 注册表设置。 CategoryOptions 的默认设置是使用特定于类别的共享的内存;但是，可以更改 CategoryOptions 若要指示应使用全局共享的内存。  
  
 包含 CategoryOptions 设置的注册表项是 HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\\< categoryName\>\Performance。 默认情况下，CategoryOptions 设置为 3，它指示 PerfCounter.dll 为使用特定于类别的共享的内存。 如果 CategoryOptions 设置为 0，PerfCounter.dll 使用全局共享的内存。 仅当要创建的实例的名称是与实例被重复使用相同，则会重复使用实例数据。 所有版本将都能够写入该类别。 如果 CategoryOptions 设置为 1，则使用全局共享的内存，但可以重复使用实例数据，类别名称是否被重复使用的类别相同的长度。  
  
 0 和 1 的设置可能会导致内存泄漏和性能计数器内存填满。  
  
## <a name="example"></a>示例  
 下面的示例演示如何指定 PerfCounter.dll 应引用 CategoryOptions 注册表条目，以确定是否应使用特定于类别的共享的内存。  
  
```xml  
<configuration>  
  <runtime>  
    <forcePerformanceCounterUniqueSharedMemoryReads enabled="true"/>  
  </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅
- [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)
- [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)
