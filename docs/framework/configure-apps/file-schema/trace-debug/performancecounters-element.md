---
title: <performanceCounters> 元素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/performanceCounters
- http://schemas.microsoft.com/.NetConfiguration/v2.0#performanceCounters
helpviewer_keywords:
- performanceCounters element
- <performanceCounters> element
ms.assetid: a71f605b-c7d9-4501-a5c3-abcbb964a43f
ms.openlocfilehash: 6144bcbda69b2ba799e87c3e7fa2118fbe4d9bf6
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57357074"
---
# <a name="performancecounters-element"></a>\<performanceCounters > 元素

指定由性能计数器共享的全局内存的大小。

 \<configuration>\
\<system.diagnostics>\
\<performanceCounters>

## <a name="syntax"></a>语法

```xml
<performanceCounters filemappingsize="524288" />
```

## <a name="attributes-and-elements"></a>特性和元素

下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|filemappingsize|必需的特性。<br /><br /> 指定的大小，以字节为单位的性能计数器共享的全局内存。 默认值为 524288。|

### <a name="child-elements"></a>子元素

无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|`Configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|
|`system.diagnostics`|为 ASP.NET 配置节指定根元素。|

## <a name="remarks"></a>备注

性能计数器使用内存映射文件或共享的内存，发布性能数据。  共享内存的大小决定可以在一次使用多少个实例。  有两种类型的共享内存： 全局共享内存和单独的共享的内存。  使用.NET framework 1.0 或 1.1 版安装的所有性能计数器类别都使用全局共享的内存。  安装.NET framework 2.0 版的性能计数器类别使用单独的共享的内存，每个性能计数器类别都有自己的内存。

可以仅使用配置文件设置全局共享内存的大小。  默认大小为 524288 字节，最大大小是 33554432 字节的最小大小为 32,768 字节。  由于全局共享的内存中共享的所有进程和类别时，第一个创建者指定的大小。  如果在应用程序配置文件中定义的大小，如果你的应用程序是会导致要执行的性能计数器的第一个应用程序才会使用该大小。  因此正确的位置来指定`filemappingsize`值是 Machine.config 文件。  不能由单个性能计数器，因此，最终全局共享的内存已用尽，如果将创建大量具有不同名称的性能计数器实例的发布中全局共享内存的内存。

对于单独共享内存的大小，在注册表中的 DWORD FileMappingSize 值密钥 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\\*\<类别名称 >* \Performance 引用首先后, 跟为全局共享内存配置文件中指定的值。 如果 FileMappingSize 值不存在，则单独的共享的内存大小设置为一个第四个 (1/4) 配置文件中的全局设置。

## <a name="see-also"></a>请参阅

- <xref:System.Diagnostics.PerformanceCounter>
- <xref:System.Diagnostics.PerformanceCounterCategory>
- <xref:System.Diagnostics.PerformanceCounter.InstanceLifetime%2A>
- <xref:System.Diagnostics.PerformanceCounterInstanceLifetime>
