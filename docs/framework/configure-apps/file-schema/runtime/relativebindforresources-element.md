---
title: <relativeBindForResources> 元素
ms.date: 03/30/2017
helpviewer_keywords:
- RelativeBindForResources element
- <relativeBindForResources> element
ms.assetid: 846ffa47-7257-4ce3-8cac-7ff627e0e34f
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 51129f9bb3a278d32a5da723dcc339f5e918c0f4
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55289804"
---
# <a name="relativebindforresources-element"></a>\<relativeBindForResources > 元素
优化附属程序集的探测。  
  
 \<配置 > 元素  
\<运行时 > 元素  
\<relativeBindForResources > 元素  
  
## <a name="syntax"></a>语法  
  
```xml
<relativeBindForResources    
   enabled="true|false" />  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`enabled`|必需的特性。<br /><br /> 指定公共语言运行时是否可优化附属程序集的探测。|  
  
## <a name="enabled-attribute"></a>enabled 特性  
  
|值|描述|  
|-----------|-----------------|  
|`false`|在运行时不会优化附属程序集的探测。 这是默认值。|  
|`true`|在运行时优化附属程序集探测。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关运行时初始化选项的信息。|  
  
## <a name="remarks"></a>备注  
 一般情况下，资源管理器探测的资源，如中所述[打包和部署资源](../../../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md)主题。 这意味着，当资源管理器探测程序特定的本地化版本的资源，它可能会在全局程序集缓存中查找、 在应用程序代码基，查询 Windows 安装程序的特定于区域性的文件夹中查找的附属程序集，并引发<xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType>事件。 `<relativeBindForResources>`元素对中的资源管理器探测附属程序集的方式进行优化。 在以下情况下的资源探测时，它可以提高性能：  
  
-   当附属程序集部署在与代码程序集相同的位置。 换而言之，如果代码程序集安装在全局程序集缓存，附属程序集必须也那里安装。 如果代码程序集安装在应用程序的基本代码，那么还必须在基本代码的特定于区域性的文件夹中安装附属程序集。  
  
-   Windows 安装程序时未使用或只是偶尔使用按需安装附属程序集。  
  
-   当应用程序代码不会处理<xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType>事件。  
  
 设置`enabled`的属性`<relativeBindForResources>`元素`true`优化资源管理器的探测附属程序集，如下所示：  
  
-   它使用父代码程序集的位置来探测附属程序集。  
  
-   它不会查询 Windows 安装程序的附属程序集。  
  
-   它不会引发<xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType>事件。  
  
## <a name="see-also"></a>请参阅
- [打包和部署资源](../../../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md)
- [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)
- [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)
