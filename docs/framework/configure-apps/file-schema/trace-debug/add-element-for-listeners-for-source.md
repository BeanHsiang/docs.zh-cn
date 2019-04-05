---
title: <add> 的 <listeners> 的 <source> 元素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sources/source/listeners/add
helpviewer_keywords:
- initializeData attribute
- add element for <listeners> for <source>
- <add> element for <listeners> for <source>
ms.assetid: 4ce36ac1-81ef-48e8-b8b2-b5a5b0e2adcb
ms.openlocfilehash: ae5231f43e7c157b5250376f7ab97deccea595e5
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55277116"
---
# <a name="add-element-for-listeners-for-source"></a>\<添加 > 元素\<侦听器 > 为\<源 >
将侦听器添加到跟踪源的 `Listeners` 集合中。  
  
 \<configuration>  
\<system.diagnostics>  
\<sources>  
\<source>  
\<listeners>  
\<add>  
  
## <a name="syntax"></a>语法  
  
```xml  
<add name="name"   
  type="TraceListenerClassName, Version, Culture, PublicKeyToken"  
  initializeData="data"/>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`type`|必需属性，除非正在引用中的侦听器`sharedListeners`集合，在该方案中，只需按名称引用它 (请参阅[示例](#example))。<br /><br /> 指定的侦听器的类型。 必须使用满足要求中指定的字符串[指定完全限定的类型名称](../../../../../docs/framework/reflection-and-codedom/specifying-fully-qualified-type-names.md)。|  
|`initializeData`|可选特性。<br /><br /> 传递给构造函数为指定类的字符串。 一个<xref:System.Configuration.ConfigurationException>如果类没有构造函数采用一个字符串，则会引发。|  
|`name`|可选特性。<br /><br /> 指定侦听器的名称。|  
|`traceOutputOptions`|可选特性。<br /><br /> 指定<xref:System.Diagnostics.TraceListener.TraceOutputOptions%2A>跟踪侦听器的属性值。|  
|[自定义属性]|可选属性。<br /><br /> 指定由标识的特定于侦听器的属性的值<xref:System.Diagnostics.TraceListener.GetSupportedAttributes%2A>为该侦听器的方法。 <xref:System.Diagnostics.DelimitedListTraceListener.Delimiter%2A> 是唯一的额外属性的一个示例<xref:System.Diagnostics.DelimitedListTraceListener>类。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<filter>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/filter-element-for-add-for-listeners-for-source.md)|将筛选器添加到跟踪源的 `Listeners` 集合中的侦听器。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`system.diagnostics`|指定用于收集、存储和路由消息的跟踪侦听器以及对跟踪开关设置的级别。|  
|`sources`|包含用于启动跟踪消息的跟踪源。|  
|`source`|指定用于启动跟踪消息的跟踪源。|  
|`listeners`|指定侦听器，用于收集、 存储和路由消息。|  
  
## <a name="remarks"></a>备注  
 .NET Framework 附带的侦听器类派生<xref:System.Diagnostics.TraceListener>类。  
  
 如果未指定`name`特性，跟踪侦听器<xref:System.Diagnostics.TraceListener.Name%2A>跟踪侦听器的属性的默认值为空字符串 ("")。 如果你的应用程序只有一个侦听器，可以将其添加而无需指定一个名称，并且您可以通过指定空字符串的名称对其进行删除。 但是，如果应用程序具有多个侦听器，则应指定每个跟踪侦听器，这样就可以识别和管理各个跟踪侦听器中的唯一名称<xref:System.Diagnostics.TraceSource.Listeners%2A?displayProperty=nameWithType>集合。  
  
> [!NOTE]
>  添加多个相同类型并且具有相同的跟踪侦听器命名为只有一个跟踪侦听器中的该类型的结果并命名要添加到`Listeners`集合。 但是，您可以以编程方式添加到多个完全相同的侦听器`Listeners`集合。  
  
 值为`initializeData`属性取决于您创建的侦听器类型。 并非所有的跟踪侦听器需要你指定`initializeData`。  
  
> [!NOTE]
>  当你使用`initializeData`属性中，你可能会收到编译器警告"未声明 initializeData 属性。" 由于配置设置时根据的抽象基类进行验证，会出现此警告<xref:System.Diagnostics.TraceListener>，这不能识别`initializeData`属性。 通常情况下，可以忽略具有构造函数采用参数的跟踪侦听器实现此警告。  
  
 下表显示了随.NET Framework 中的跟踪侦听器，并说明的值及其`initializeData`属性。  
  
|跟踪侦听器类|initializeData 属性值|  
|--------------------------|------------------------------------|  
|<xref:System.Diagnostics.ConsoleTraceListener?displayProperty=nameWithType>|`useErrorStream`值<xref:System.Diagnostics.ConsoleTraceListener.%23ctor%2A>构造函数。  设置`initializeData`属性为"`true`"来写入跟踪和调试输出写入标准错误流中; 将其设置为"`false`"要写入到标准输出流。|  
|<xref:System.Diagnostics.DelimitedListTraceListener?displayProperty=nameWithType>|文件的名称<xref:System.Diagnostics.DelimitedListTraceListener>写入。|  
|<xref:System.Diagnostics.EventLogTraceListener?displayProperty=nameWithType>|现有事件日志源的名称。|  
|<xref:System.Diagnostics.EventSchemaTraceListener?displayProperty=nameWithType>|文件的名称，<xref:System.Diagnostics.EventSchemaTraceListener>写入。|  
|<xref:System.Diagnostics.TextWriterTraceListener?displayProperty=nameWithType>|文件的名称，<xref:System.Diagnostics.TextWriterTraceListener>写入。|  
|<xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=nameWithType>|文件的名称，<xref:System.Diagnostics.XmlWriterTraceListener>写入。|  
  
## <a name="configuration-file"></a>配置文件  
 计算机配置文件 (Machine.config) 和应用程序配置文件中，可以使用此元素。  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用`<add>`元素添加侦听器`console`并`textListener`到`Listeners`跟踪源集合`TraceSourceApp`。 `textListener`侦听器将跟踪输出写入到文件 myListener.log。  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="TraceSourceApp" switchName="sourceSwitch"   
        switchType="System.Diagnostics.SourceSwitch">  
        <listeners>  
          <add name="console"   
            type="System.Diagnostics.ConsoleTraceListener"/>  
          <add name="textListener"/>  
          <remove name="Default"/>  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add name="textListener"   
        type="System.Diagnostics.TextWriterTraceListener"   
        initializeData="myListener.log"/>  
    </sharedListeners>  
    <switches>  
      <add name="sourceSwitch" value="Warning"/>  
    </switches>  
  </system.diagnostics>  
</configuration>   
```  
  
## <a name="see-also"></a>请参阅
- <xref:System.Diagnostics.TraceSource>
- <xref:System.Diagnostics.TraceListener>
- [跟踪和调试设置架构](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)
- [跟踪侦听器](../../../../../docs/framework/debug-trace-profile/trace-listeners.md)
