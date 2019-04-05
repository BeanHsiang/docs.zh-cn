---
title: <startup> 元素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/startup
- http://schemas.microsoft.com/.NetConfiguration/v2.0#startup
helpviewer_keywords:
- container tags, <startup> element
- <startup> element
- startup element
ms.assetid: 536acfd8-f827-452f-838a-e14fa3b87621
ms.openlocfilehash: 5047cb0ab1c8206abd88dc795e50272d69f1fd3f
ms.sourcegitcommit: b8ace47d839f943f785b89e2fff8092b0bf8f565
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2019
ms.locfileid: "55674563"
---
# <a name="startup-element"></a>\<启动 > 元素

指定公共语言运行时启动信息。

 \<configuration> \<startup>

## <a name="syntax"></a>语法

```xml
<startup useLegacyV2RuntimeActivationPolicy="true|false" > 
</startup>
```

## <a name="attributes-and-elements"></a>特性和元素

 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|`useLegacyV2RuntimeActivationPolicy`|可选特性。<br /><br /> 指定是否启用[!INCLUDE[dnprdnext](../../../../../includes/dnprdnext-md.md)]运行时激活策略或使用[!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)]激活策略。|

## <a name="uselegacyv2runtimeactivationpolicy-attribute"></a>useLegacyV2RuntimeActivationPolicy 属性

|值|描述|
|-----------|-----------------|
|`true`|启用[!INCLUDE[dnprdnext](../../../../../includes/dnprdnext-md.md)]对于所选的运行时，它将绑定旧式运行时激活技术的运行时激活策略 (如[CorBindToRuntimeEx 函数](../../../unmanaged-api/hosting/corbindtoruntimeex-function.md)) 到运行时从配置文件而不是选择在 CLR 版本 2.0 将达到其上限。 因此，如果从配置文件选择 CLR 版本 4 或更高版本，则使用.NET Framework 的早期版本创建的混合模式程序集是加载与所选的 CLR 版本。 设置此值可防止 CLR 版本 1.1 或 CLR 版本 2.0 加载到同一个进程，有效地禁用进程内并行的功能。|
|`false`|使用的默认激活策略[!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)]和更高版本，这是允许旧的运行时加载到进程的 CLR 版本 1.1 或 2.0 的激活方法。 将设置此值可阻止混合模式程序集加载到.NET Framework 4 或更高版本，除非在.NET Framework 4 或更高版本生成它们。 此值是默认值。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|[\<requiredRuntime>](requiredruntime-element.md)|指定应用程序仅支持 1.0 版本的公共语言运行时。 运行时 1.1 版或更高版本构建的应用程序应使用 **\<supportedRuntime >** 元素。|
|[\<supportedRuntime>](supportedruntime-element.md)|指定应用程序支持的公共语言运行时版本。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|

## <a name="remarks"></a>备注

 **\<SupportedRuntime>** 元素应由使用 1.1 版或更高版本的运行时版本生成的所有应用程序。 仅支持 1.0 版的运行时生成的应用程序必须使用 **\<requiredRuntime >** 元素。

 在 Microsoft Internet Explorer 中托管的应用程序的启动代码将忽略**\<启动 >** 元素和子元素。

## <a name="the-uselegacyv2runtimeactivationpolicy-attribute"></a>UseLegacyV2RuntimeActivationPolicy 属性

 此特性会非常有用，如果你的应用程序使用旧式激活路径，例如[CorBindToRuntimeEx 函数](../../../unmanaged-api/hosting/corbindtoruntimeex-function.md)，并且希望这些路径来激活而不是早期版本的 CLR 版本 4 或如果你的应用程序使用生成[!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)]但在使用.NET Framework 的早期版本构建的混合模式程序集具有依赖项。 在这些情况下，将属性设置为`true`。

> [!NOTE]
> 将属性设置为`true`防止 CLR 版本 1.1 或 CLR 版本 2.0 加载到同一个进程，有效地禁用进程内并行的功能 (请参阅[COM 互操作的并行执行](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/8t8td04t(v=vs.100)))。

## <a name="example"></a>示例

 下面的示例演示如何在配置文件中指定的运行时版本。

```xml
<!-- When used with version 1.0 of the .NET Framework runtime -->
<configuration>
   <startup>
      <requiredRuntime version="v1.0.3705" safemode="true"/>
   </startup>
</configuration>
<!-- When used with version 1.1 (or later) of the runtime -->
<configuration>
   <startup>
      <supportedRuntime version="v1.1.4322"/>
      <supportedRuntime version="v1.0.3705"/>
   </startup>
</configuration>
```

## <a name="see-also"></a>请参阅

- [启动设置架构](index.md)
- [配置文件架构](../index.md)
- [如何：将应用配置为支持 .NET Framework 4 或更高版本](../../../migration-guide/how-to-configure-an-app-to-support-net-framework-4-or-4-5.md)
- [COM 互操作的的并行执行](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/8t8td04t(v=vs.100))
- [进程内并行执行](../../../deployment/in-process-side-by-side-execution.md)