---
title: <Library>元素 (.NET Native)
ms.date: 03/30/2017
ms.assetid: f642276b-33fb-4a81-b882-8808c31ba69e
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7f2de27152200ed07e5f82b5dc08613451c7aa25
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55284903"
---
# <a name="library-element-net-native"></a>\<库 > 元素 (.NET Native)
定义包含元数据在运行时间可以用于反射的类型和类型成员的程序集。  
  
 \<Directives> 元素  
\<Library> 元素  
  
## <a name="syntax"></a>语法  
  
```xml  
<Library Name="assembly_name" />  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`Name`|必需的特性。 指定一个程序集的名称。 这个 `<Library>` 元素的子元素为在这个程序集中找到的类型和类型成员定义运行时反射策略。|  
  
## <a name="name-attribute"></a>Name 特性  
  
|值|描述|  
|-----------|-----------------|  
|assembly_name|程序集的简单名称，不要包含文件扩展名。 此特性对应 <xref:System.Reflection.AssemblyName.Name%2A?displayProperty=nameWithType> 属性。 例如，一个名为 Extensions.dll 的程序集的名称为“Extensions”。 参阅“备注”部分，了解支持对来自程序集的元数据有条件包含的 assembly_name 的一种特殊形式。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<Assembly>](../../../docs/framework/net-native/assembly-element-net-native.md)|将策略应用到特定程序集中的所有类型。|  
|[\<Namespace>](../../../docs/framework/net-native/namespace-element-net-native.md)|将策略应用到特定命名空间中的所有类型。|  
|[\<Type>](../../../docs/framework/net-native/type-element-net-native.md)|将策略应用到一个特定类型，例如一个类或结构。|  
|[\<TypeInstantiation>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md)|将策略应用到一个构造泛型类型。 例如，一个 [\<TypeInstantiation>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md) 元素可用于为一个 `List<String>` 类型定义策略。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<Directives>](../../../docs/framework/net-native/directives-element-net-native.md)|运行时指令文件的根元素。|  
  
## <a name="remarks"></a>备注  
 [\<Directives>](../../../docs/framework/net-native/directives-element-net-native.md) 元素可包括零个、一个或多个 `<Library>` 元素。  
  
 `<Library>` 元素充当容器，用来定义其元数据在运行时间需要存在的程序元素；此元素不表示策略。 在编译时间，编译器工具仅搜索由 `<Library>` 元素指定的库，以查找其子元素识别出的程序元素。 相比而言，编译器工具搜索 .NET Framework 核心库等所有库，以查找由 [\<Application>](../../../docs/framework/net-native/application-element-net-native.md) 元素识别出的子元素。  
  
 `<Library>` 指令可以有条件地使用。 如果的名称`<Library>`元素开始和结束的星号 (\*)，则`<Library>`指令仅在星号之间指定的程序集引用的应用程序有影响。 例如，以下运行时指令仅在 Utillities.dll 程序库被应用引用时才适用。  
  
```xml  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
  <Library Name="*Utilities*">  
   ...  
  </Library>  
</Directives>  
```  
  
## <a name="see-also"></a>请参阅
- [\<应用程序 > 元素](../../../docs/framework/net-native/application-element-net-native.md)
- [\<指令 > 元素](../../../docs/framework/net-native/directives-element-net-native.md)
- [运行时指令 (rd.xml) 配置文件参考](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)
- [运行时指令元素](../../../docs/framework/net-native/runtime-directive-elements.md)
