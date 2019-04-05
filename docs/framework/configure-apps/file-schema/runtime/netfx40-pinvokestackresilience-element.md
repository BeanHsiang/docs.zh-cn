---
title: < NetFx40_PInvokeStackResilience > 元素
ms.date: 03/30/2017
helpviewer_keywords:
- <NetFx40_PInvokeStackResilience> element
- NetFx40_PInvokeStackResilience element
ms.assetid: 39fb1588-72a4-4479-af74-0605233b68bd
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8bc0d7c9222c31900cad9a8be05c79f7f8a04719
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55289336"
---
# <a name="netfx40pinvokestackresilience-element"></a>\<NetFx40_PInvokeStackResilience > 元素
指定运行时是否以减慢托管和非托管代码之间的转换速度为代价，在运行时自动修复不正确的平台调用声明。  
  
 \<configuration>  
\<运行时 >  
<NetFx40_PInvokeStackResilience>  
  
## <a name="syntax"></a>语法  
  
```xml  
<NetFx40_PInvokeStackResilience  enabled="1|0"/>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`enabled`|必需的特性。<br /><br /> 指定是否在运行时检测到不正确的平台调用声明和 32 位平台上，将自动修复在运行时堆栈。|  
  
## <a name="enabled-attribute"></a>enabled 特性  
  
|值|描述|  
|-----------|-----------------|  
|`0`|运行时使用的更快的互操作封送处理体系结构中引入[!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)]，这不会检测和修复不正确的平台调用声明。 这是默认设置。|  
|`1`|运行时使用的转换速度的检测和修复不正确的平台调用声明。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关运行时初始化选项的信息。|  
  
## <a name="remarks"></a>备注  
 此元素可以交换更快地互操作封送处理运行时恢复能力对不正确的平台调用声明。  
  
 从开始[!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)]，简化的互操作封送处理体系结构提供了从托管代码转换到非托管代码一显著的性能改进。 在早期版本的.NET Framework，封送处理层检测到不正确的平台调用在 32 位平台上的声明，并自动修复堆栈。 新的封送处理体系结构消除了此步骤。 因此，转换速度非常快，但不正确的平台调用声明可能会导致程序失败。  
  
 为了更加轻松地在开发过程中检测不正确的声明，改进 Visual Studio 调试体验。 [PInvokeStackImbalance](../../../../../docs/framework/debug-trace-profile/pinvokestackimbalance-mda.md)托管调试助手 (MDA) 通知你的应用程序运行带有附加调试程序时，您不正确的平台调用声明。  
  
 为应用程序使用组件，则不能重新编译，和，具有不正确的平台调用声明，您可以使用其中的解决情况`NetFx40_PInvokeStackResilience`元素。 将此元素添加到应用程序配置文件与`enabled="1"`opts 到与早期版本的.NET Framework 中，转换速度为代价的行为的兼容性模式。 已针对.NET Framework 的早期版本编译的程序集自动选择加入此兼容性模式，并且不需要此元素。  
  
## <a name="configuration-file"></a>配置文件  
 仅在应用程序配置文件中，可以使用此元素。  
  
## <a name="example"></a>示例  
 下面的示例演示如何对不正确的增强恢复能力选择使用平台调用声明应用程序之间的转换速度为代价托管和非托管代码。  
  
```xml  
<configuration>  
   <runtime>  
      <NetFx40_PInvokeStackResilience enabled="1"/>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅
- [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)
- [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)
- [pInvokeStackImbalance](../../../../../docs/framework/debug-trace-profile/pinvokestackimbalance-mda.md)
