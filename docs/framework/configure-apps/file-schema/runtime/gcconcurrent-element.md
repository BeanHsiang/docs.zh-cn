---
title: <gcConcurrent> 元素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/gcConcurrent
- http://schemas.microsoft.com/.NetConfiguration/v2.0#gcConcurrent
helpviewer_keywords:
- container tags, <gcConcurrent> element
- gcConcurrent element
- <gcConcurrent> element
ms.assetid: 503f55ba-26ed-45ac-a2ea-caf994da04cd
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0e2be4d9384f1e1ef73ce6064184aa2621a517a8
ms.sourcegitcommit: b8ace47d839f943f785b89e2fff8092b0bf8f565
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2019
ms.locfileid: "55674589"
---
# <a name="gcconcurrent-element"></a>\<gcConcurrent > 元素

指定公共语言运行时是否在单独线程上运行垃圾回收。

\<configuration>\
\<runtime>\
\<gcConcurrent>

## <a name="syntax"></a>语法

```xml
<gcConcurrent
   enabled="true|false"/>
```

## <a name="attributes-and-elements"></a>特性和元素

下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|`enabled`|必需的特性。<br /><br /> 指定运行时是否并发运行服务器垃圾回收。|

## <a name="enabled-attribute"></a>已启用的属性

|值|描述|
|-----------|-----------------|
|`false`|不会同时运行垃圾回收。|
|`true`|并发运行垃圾回收。 这是默认设置。|

### <a name="child-elements"></a>子元素

无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|

## <a name="remarks"></a>备注

在.NET Framework 4 之前，工作站垃圾回收支持并发垃圾回收，在后台对一个单独线程执行垃圾回收。 在.NET Framework 4 中，并发垃圾回收被后台 GC 取代，它还在单独的线程上在后台中执行垃圾回收。 从 .NET Framework 4.5 开始，服务器垃圾回收可提供后台垃圾回收。 `<gcConcurrent>`元素控制运行时是否执行并发还是后台垃圾回收，如果可用，或是否在前台执行垃圾回收。

### <a name="to-disable-background-garbage-collection"></a>若要禁用后台垃圾回收

> [!WARNING]
> 从.NET Framework 4 开始，并发垃圾回收替换为后台垃圾回收。 条款*并发*并*背景*.NET Framework 文档中互换使用。 若要禁用后台垃圾回收，请使用 `<gcConcurrent>` 元素，如本文所述。

默认情况下，运行时使用并发或后台垃圾回收，回收针对延迟进行了优化。 如果应用程序涉及大量用户交互，则通过让并发垃圾回收保持启用状态，可最大限度缩短应用程序执行垃圾回收时的暂停时间。 如果将 `enabled` 元素的 `<gcConcurrent>` 特性设置为 `false`，运行时将使用针对吞吐量优化的非并发垃圾回收。 下列配置文件会禁用后台垃圾回收。

```xml
<configuration>
   <runtime>
      <gcConcurrent enabled="false"/>
   </runtime>
</configuration>
```

 如果没有`<gcConcurrentSetting>`设置计算机配置文件中，它定义所有.NET Framework 应用程序的默认值。 计算机配置文件设置将重写应用程序配置文件设置。

 有关详细信息并发和后台垃圾回收，请参阅[并发垃圾回收](../../../../standard/garbage-collection/fundamentals.md#concurrent-garbage-collection)主题中[垃圾回收的基础](../../../../standard/garbage-collection/fundamentals.md)一文。

## <a name="example"></a>示例

下面的示例启用并发垃圾回收：

```xml
<configuration>
   <runtime>
      <gcConcurrent enabled="true"/>
   </runtime>
</configuration>
```

## <a name="see-also"></a>请参阅

- [运行时设置架构](index.md)
- [配置文件架构](../index.md)
- [垃圾回收的基础知识](../../../../standard/garbage-collection/fundamentals.md)
