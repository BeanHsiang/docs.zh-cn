---
title: <filter>
ms.date: 03/30/2017
ms.assetid: 3266700b-904b-44e4-93a7-e06a1a445100
ms.openlocfilehash: bff19f106d86c73dea80b8b57bb73442eaa2cf9f
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55278780"
---
# <a name="filter"></a>\<filter>

定义路由筛选器，确定类型的 Windows Communication Foundation (WCF)<xref:System.ServiceModel.Dispatcher.MessageFilter>若要在评估传入消息，以及任何支持的数据和所需的筛选器参数时使用。

\<system.serviceModel> \<routing> \<filters> \<filter>
  
## <a name="syntax"></a>语法  
  
```xml  
<routing>
  <filters>
    <filter customType="String"
            filterData="String"
            filterType="Action/Address/AddressPrefix/And/Custom/Endpoint/MatchAll/XPath"
            name="String" />
  </filters>
</routing>
```  
  
## <a name="attributes-and-elements"></a>特性和元素

下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

| 特性  | 描述 |
| ---------- | ----------- |
| customType | 一个字符串，包含要用作筛选器的自定义类型的完全限定类型名称。 如果`filterType`设置为`custom`，该属性包含要创建的类的完全限定的类型名称。  `filterData` 此外可能包含对自定义类型筛选器求值期间使用的值。 |
| filterData | 一个包含筛选器数据的字符串。 有关如何指定此特性的更多信息，请参见 <xref:System.ServiceModel.Routing.Configuration.FilterElement.FilterData%2A>。 |
| filterType | 一个包含筛选器类型的字符串。 此特性的类型为 <xref:System.ServiceModel.Routing.Configuration.FilterType>。  有关如何使用此 `filterData` 特性的更多信息，请参见 <xref:System.ServiceModel.Routing.Configuration.FilterElement.FilterData%2A>。 |
| name       | 一个字符串，包含此筛选器元素的唯一名称。 |

### <a name="child-elements"></a>子元素

无。

### <a name="parent-elements"></a>父元素

| 元素 | 描述 |
| ------- | ----------- |
| [\<routing>](../../../../../docs/framework/configure-apps/file-schema/wcf/routing.md) | 用于定义一组路由筛选器，确定类型的 Windows Communication Foundation (WCF) 的配置节<xref:System.ServiceModel.Dispatcher.MessageFilter>要评估传入消息时使用。 |

## <a name="see-also"></a>请参阅

- <xref:System.ServiceModel.Routing.Configuration.FilterElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Routing.Configuration.FilterElement.FilterData%2A?displayProperty=nameWithType>
- <xref:System.ServiceModel.Routing.Configuration.FilterType?displayProperty=nameWithType>
