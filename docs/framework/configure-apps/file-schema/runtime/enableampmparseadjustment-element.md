---
title: <EnableAmPmParseAdjustment> 元素
ms.date: 03/30/2017
ms.assetid: fda998a5-f538-4f8b-a18c-ee7f35e16938
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b3316184aaa624fffdd18f472a7f3a709b42045a
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55269206"
---
# <a name="enableampmparseadjustment-element"></a>\<EnableAmPmParseAdjustment > 元素
确定是否日期和时间分析方法使用调整后的规则集来分析日期字符串包含天、 月、 小时和 AM/PM 指示符。  
  
 \<configuration>  
 \<运行时 >  
\<EnableAmPmParseAdjustment>  
  
## <a name="syntax"></a>语法  
  
```xml  
<EnableAmPmParseAdjustment enabled="0"|"1" />  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`enabled`|必需的特性。<br /><br /> 指定是否日期和时间分析方法使用调整后的规则集来分析日期字符串包含仅日、 月、 小时和 AM/PM 指示符。|  
  
### <a name="enabled-attribute"></a>enabled 特性  
  
|值|描述|  
|-----------|-----------------|  
|0|日期和时间分析方法不使用调整后的规则用于分析包含仅日、 月、 小时和 AM/PM 指示符的日期字符串。|  
|1|日期和时间分析方法的分析包含仅日、 月、 小时和 AM/PM 指示符的日期字符串使用调整后的规则。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关运行时初始化选项的信息。|  
  
## <a name="remarks"></a>备注  
 `<EnableAmPmParseAdjustment>`元素控制以下方法如何分析日期字符串，其中包含日期和月份后, 跟一小时和 AM/PM 指示符 （如"4/10 6 AM"):  
  
-   <xref:System.DateTime.Parse%2A?displayProperty=nameWithType>  
  
-   <xref:System.DateTimeOffset.Parse%2A?displayProperty=nameWithType>  
  
-   <xref:System.DateTime.TryParse%2A?displayProperty=nameWithType>  
  
-   <xref:System.DateTimeOffset.TryParse%2A?displayProperty=nameWithType>  
  
-   <xref:System.Convert.ToDateTime%2A?displayProperty=nameWithType>  
  
 没有其他模式会受到影响。  
  
 `<EnableAmPmParseAdjustment>`元素不起任何作用<xref:System.DateTime.ParseExact%2A?displayProperty=nameWithType>， <xref:System.DateTime.TryParseExact%2A?displayProperty=nameWithType>， <xref:System.DateTimeOffset.ParseExact%2A?displayProperty=nameWithType>，和<xref:System.DateTimeOffset.TryParseExact%2A?displayProperty=nameWithType>方法。  
  
> [!IMPORTANT]
>  在.NET Core 和.NET Native，默认情况下启用的调整后的 AM/PM 分析规则。   
  
 如果分析的调整规则未启用，该字符串的第一个数字解释为 12 小时制时钟的小时和 AM/PM 指示符除外的字符串的其余部分将被忽略。 日期和时间分析方法返回包含当前日期和从日期字符串中提取一天的小时。  
  
 如果启用了分析的调整规则，分析方法的日期和月份为属于当前年份，解释和解释为 12 小时制的小时的时间。  
  
 下表说明了中的差异<xref:System.DateTime>值时<xref:System.DateTime.Parse%28System.String%29?displayProperty=nameWithType>方法用于分析字符串""4/10 6 AM"与`<EnableAmPmParseAdjustment>`元素的`enabled`属性设置为"0"或"1"。 它假定今天的日期为 2017 年 1 月 5 日，并像使用特定的区域性的"G"格式字符串格式化显示的日期。  
  
|区域性名称|enabled="0"|enabled="1"|  
|------------------|------------------|------------------|  
|en-US|2017 年 1 月 5 日 4:00:00 AM|2017 年 4 月 10 日上午 6:00:00|  
|en-GB|5/1/2017 6:00:00|10/4/2017 6:00:00|  
  
## <a name="see-also"></a>请参阅
- [\<运行时 > 元素](../../../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md)
- [\<configuration> 元素](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)
