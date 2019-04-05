---
title: <supportedRuntime> 元素
ms.date: 04/10/2018
ms.custom: updateeachrelease
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#supportedRuntime
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/startup/supportedRuntime
helpviewer_keywords:
- supportedRuntime element
- <supportedRuntime> element
ms.assetid: 1ae16e23-afbe-4de4-b413-bc457f37b69f
ms.openlocfilehash: 93e69290062e1b82dddbb68f7a139763695a42fb
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55271767"
---
# <a name="supportedruntime-element"></a>\<supportedRuntime > 元素

指定应用程序支持的公共语言运行时版本。 此元素应由用 .NET Framework 1.1 版或更高版本生成的所有应用程序使用。  
  
[\<configuration>](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)  
&nbsp;&nbsp;[\<startup>](../../../../../docs/framework/configure-apps/file-schema/startup/startup-element.md)  
&nbsp;&nbsp;&nbsp;&nbsp;**\<supportedRuntime>**  
  
## <a name="syntax"></a>语法
  
```xml  
<supportedRuntime version="runtime version" sku="sku id"/>  
```  
  
## <a name="attributes"></a>特性
  
|特性|描述|  
|---------------|-----------------|  
|**版本**|可选特性。<br /><br /> 一个字符串值，它指定此应用程序支持的公共语言运行时 (CLR) 版本。 有关的有效值`version`属性，请参阅["运行时版本"值](#version)部分。 **注意：** 通过.NET Framework 3.5"*运行时版本*"值的形式*主要*。*次要*。*生成*。 从 [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)] 开始，仅主版本号和次版本号是必需的（即“v4.0”而不是“v4.0.30319”）。 建议使用较短字符串。|  
|**sku**|可选特性。<br /><br /> 一个字符串值，该值指定库存单位 (SKU)，库存单位则指定此应用程序支持的 .NET Framework 版本。<br /><br /> 从 .NET Framework 4.0 起，建议使用 `sku` 特性。  若存在该特性，则它指示应用面向的 .NET Framework 版本。<br /><br /> 有关有效的 sku 属性的值，请参阅["sku id"值](#sku)部分。|  
  
## <a name="remarks"></a>备注

如果 **\<supportedRuntime>** 元素不存在应用程序配置文件，请使用用于生成应用程序的运行时的版本。  

**\<SupportedRuntime>** 元素应由使用 1.1 版或更高版本的运行时版本生成的所有应用程序。 仅支持 1.0 版的运行时生成的应用程序必须使用[ \<requiredRuntime >](../../../../../docs/framework/configure-apps/file-schema/startup/requiredruntime-element.md)元素。  
  
> [!NOTE]
>  如果您使用[CorBindToRuntimeByCfg](../../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimebycfg-function.md)函数以指定配置文件，则必须使用`<requiredRuntime>`所有版本的运行时的元素。 `<supportedRuntime>`使用时，将忽略元素[CorBindToRuntimeByCfg](../../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimebycfg-function.md)。  
  
对于支持从 .NET Framework 1.1 到 3.5 的运行时版本的应用，支持多个运行时版本时，第一个元素应指定优先级最高的版本，最后一个元素应指定优先级最低的版本。 对于支持 .NET Framework 4.0 或更高版本的应用，`version` 特性指示普遍适用于 .NET Framework 4 及更高版本的 CLR 版本，而 `sku` 特性指示应用所面向的单个 .NET Framework 版本。  
  
> [!NOTE]
>  如果你的应用程序使用旧式激活路径，如[CorBindToRuntimeEx 函数](../../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md)，并且希望这些路径来激活而不是早期版本的 CLR 版本 4 或如果你的应用程序使用生成[!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)]具有依赖关系，但在上使用.NET Framework 的早期版本构建的混合模式程序集，它不是只需指定[!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)]在受支持运行时列表中。 此外，在[\<启动 > 元素](../../../../../docs/framework/configure-apps/file-schema/startup/startup-element.md)在配置文件中，必须设置`useLegacyV2RuntimeActivationPolicy`归于`true`。 但是，将此特性设置为 `true` 意味着，用 .NET Framework 早期版本生成的所有组件都使用 [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)]（而不是生成它们时所用的运行时）运行。  
  
我们建议你使用应用程序可在其上运行的所有 .NET Framework 版本来测试这些应用程序。  
  
<a name="version"></a>   
## <a name="runtime-version-values"></a>“运行时版本”值  
`runtime`属性指定给定应用程序所需的公共语言运行时 (CLR) 版本。 请注意，所有.NET Framework v4.x 版本都指定`v4.0`CLR。 下表列出了有效值*运行时版本*的值`version`属性。  

|.NET Framework 版本|`version` 特性|  
|----------------------------|-------------------------|  
|1.0|"v1.0.3705"|  
|1.1|"v1.1.4322"|  
|2.0|"v2.0.50727"|  
|3.0|"v2.0.50727"|  
|3.5|"v2.0.50727"|  
|4.0-4.7.2|"v4.0"|  

<a name="sku"></a>   
## <a name="sku-id-values"></a>“SKU ID”值

`sku`特性使用目标框架名字对象 (TFM) 以指示应用所面向并运行所需的.NET framework 版本。 下表列出了受支持的有效值`sku`属性，从.NET Framework 4 开始。
  
|.NET Framework 版本|`sku` 特性|  
|----------------------------|---------------------|  
|4.0|".NETFramework,Version=v4.0"|  
|4.0，客户端配置文件|".NETFramework,Version=v4.0,Profile=Client"|  
|4.0，平台更新 1|".NETFramework,Version=v4.0.1"|  
|4.0，客户端配置文件，Update 1|".NETFramework,Version=v4.0.1,Profile=Client"|  
|4.0，平台更新 2|".NETFramework,Version=v4.0.2"|  
|4.0，客户端配置文件，Update 2|".NETFramework,Version=v4.0.2,Profile=Client"|  
|4.0，平台更新 3|".NETFramework,Version=v4.0.3"|  
|4.0，客户端配置文件，Update 3|".NETFramework,Version=v4.0.3,Profile=Client"|  
|4.5|".NETFramework,Version=v4.5"|  
|4.5.1|".NETFramework,Version=v4.5"|  
|4.5.2|".NETFramework,Version=v4.5"|  
|4.6|".NETFramework,Version=v4.5"|  
|4.6.1|".NETFramework,Version=v4.5"|  
|4.6.2|".NETFramework,Version=v4.6.2"|  
|4.7|".NETFramework,Version=v4.7"|
|4.7.1|".NETFramework,Version=v4.7.1"|
|4.7.2|".NETFramework，版本 = v4.7.2"|

## <a name="example"></a>示例  
 下面的示例演示如何在配置文件中指定支持的运行时版本。 配置文件指示应用面向.NET Framework 4.7。  
  
```xml  
<configuration>  
   <startup>  
      <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7" />  
   </startup>  
</configuration>  
```  
  
## <a name="configuration-file"></a>配置文件

此元素可用于应用程序配置文件中。

## <a name="see-also"></a>请参阅

- [启动设置架构](../../../../../docs/framework/configure-apps/file-schema/startup/index.md)
- [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)
- [进程内并行执行](../../../../../docs/framework/deployment/in-process-side-by-side-execution.md)
