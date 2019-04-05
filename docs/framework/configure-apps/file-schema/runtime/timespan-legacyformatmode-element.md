---
title: <TimeSpan_LegacyFormatMode> Element
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- <TimeSpan_LegacyFormatMode> element
- TimeSpan_LegacyFormatMode element
ms.assetid: 865e7207-d050-4442-b574-57ea29d5e2d6
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f3f18d5e62f4986f880b35825d8e0239dba8d4c6
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55277740"
---
# <a name="timespanlegacyformatmode-element"></a>\<TimeSpan_LegacyFormatMode > 元素
确定运行时是否保留旧行为中的格式设置操作<xref:System.TimeSpan?displayProperty=nameWithType>值。  
  
 \<configuration>  
\<运行时 >  
<TimeSpan_LegacyFormatMode>  
  
## <a name="syntax"></a>语法  
  
```xml  
<TimeSpan_LegacyFormatMode    
   enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`enabled`|必需的特性。<br /><br /> 指定运行时是否使用旧式格式设置行为与<xref:System.TimeSpan?displayProperty=nameWithType>值。|  
  
## <a name="enabled-attribute"></a>enabled 特性  
  
|值|描述|  
|-----------|-----------------|  
|`false`|在运行时不会还原旧的格式设置行为。|  
|`true`|在运行时将还原旧的格式设置行为。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关运行时初始化选项的信息。|  
  
## <a name="remarks"></a>备注  
 从开始[!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)]，则<xref:System.TimeSpan?displayProperty=nameWithType>结构实现<xref:System.IFormattable>接口并支持格式设置操作与标准和自定义格式字符串。 如果分析方法遇到了不受支持的格式说明符或格式字符串，则会引发<xref:System.FormatException>。  
  
 在以前版本的.NET Framework<xref:System.TimeSpan>结构未实现<xref:System.IFormattable>，并且不支持格式字符串。 但是，许多开发人员错误地假定<xref:System.TimeSpan>并支持一组格式字符串并使用它们在[复合格式设置操作](../../../../../docs/standard/base-types/composite-formatting.md)等方法与<xref:System.String.Format%2A?displayProperty=nameWithType>。 通常，如果某个类型实现<xref:System.IFormattable>并支持格式字符串，调用格式设置方法与不受支持格式字符串通常引发<xref:System.FormatException>。 但是，由于<xref:System.TimeSpan>未实现<xref:System.IFormattable>，运行时忽略格式字符串，并改为调用<xref:System.TimeSpan.ToString?displayProperty=nameWithType>方法。 这意味着，尽管格式字符串，格式设置操作没有影响，但是它们的存在没有导致<xref:System.FormatException>。  
  
 对于在其中旧代码将传递的复合格式设置方法，并为无效格式字符串，而不能重新编译该代码的情况下，你可以使用`<TimeSpan_LegacyFormatMode>`元素来还原旧<xref:System.TimeSpan>行为。 当您将设置`enabled`到此元素的特性`true`、 复合格式设置方法的调用中的结果<xref:System.TimeSpan.ToString?displayProperty=nameWithType>而非<xref:System.TimeSpan.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType>，和一个<xref:System.FormatException>不会引发。  
  
## <a name="example"></a>示例  
 下面的示例实例化<xref:System.TimeSpan>对象，并尝试将其与格式化<xref:System.String.Format%28System.String%2CSystem.Object%29?displayProperty=nameWithType>使用不受支持的标准格式字符串的方法。  
  
 [!code-csharp[TimeSpan.BreakingChanges#1](../../../../../samples/snippets/csharp/VS_Snippets_CLR/timespan.breakingchanges/cs/legacyformatmode1.cs#1)]
 [!code-vb[TimeSpan.BreakingChanges#1](../../../../../samples/snippets/visualbasic/VS_Snippets_CLR/timespan.breakingchanges/vb/legacyformatmode1.vb#1)]  
  
 上运行此示例[!INCLUDE[net_v35_short](../../../../../includes/net-v35-short-md.md)]或在较早版本，它会显示以下输出：  
  
```  
12:30:45  
```  
  
 如果在 [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)] 或以后版本上运行此示例，则输出将与此处的输出明显不同：  
  
```  
Invalid Format  
```  
  
 但是，如果将下面的配置文件添加到示例的目录中，然后在 [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)] 或更高版本上运行此示例，则输出将与示例在 [!INCLUDE[net_v35_short](../../../../../includes/net-v35-short-md.md)] 上运行时产生的输出相同。  
  
```xml  
<?xml version ="1.0"?>  
<configuration>  
   <runtime>  
      <TimeSpan_LegacyFormatMode enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅
- [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)
- [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)
