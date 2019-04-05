---
title: <codeBase> 元素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#codeBase
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding/dependentAssembly/codeBase
helpviewer_keywords:
- <codeBase> element
- container tags, <codeBase> element
- codeBase element
ms.assetid: d48a3983-2297-43ff-a14d-1f29d3995822
ms.openlocfilehash: b5825efcc613689e73fb56b6695fe7c75ff09136
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57356606"
---
# <a name="codebase-element"></a>\<b a s e > 元素

指定公共语言运行时在哪里可以找到程序集。

\<configuration> \<runtime> \<assemblyBinding> \<dependentAssembly> \<codeBase>

## <a name="syntax"></a>语法

```xml
   <codeBase
        version="Assembly version"
        href="URL of assembly"/>
```

## <a name="attributes-and-elements"></a>特性和元素

下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|`href`|必需的特性。<br /><br /> 指定运行时在哪里可以找到程序集的指定的版本的 URL。|
|`version`|必需的特性。<br /><br /> 指定基本代码适用于程序集的版本。 程序集版本号的格式*major.minor.build.revision*。|

## <a name="version-attribute"></a>版本属性

|值|描述|
|-----------|-----------------|
|每个部分的版本号的有效值为 0 到 65535。|不适用。|

### <a name="child-elements"></a>子元素

无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|`buildproviders`|定义用于编译自定义资源文件的生成提供程序的集合。 您可以拥有任意数量的生成提供程序。|
|`compilation`|配置 ASP.NET 使用的所有编译设置。|
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|
|`System.web`|为 ASP.NET 配置节指定根元素。|

## <a name="remarks"></a>备注

运行时要使用 **\<b a s e >** 设置计算机配置文件或发布服务器策略文件中，该文件还必须重定向程序集版本。 应用程序配置文件而无需将程序集版本重定向有基本代码设置。 在确定要使用的程序集版本之后, 运行时应用确定版本的文件的基本代码设置。 如果指示没有基本代码，运行时探测程序集以通常的方式。

如果该程序集具有强名称，基本代码设置可以是任意位置在本地 intranet 或 Internet 上。 如果程序集私有程序集，基本代码设置必须为应用程序的目录的相对路径。

对于没有强名称程序集，则忽略版本和加载程序将使用出现的第一个\<o d e b > 内\<dependentAssembly >。 如果在将绑定重定向到另一个程序集的应用程序配置文件中没有条目，因此重定向即使程序集版本不匹配绑定请求将优先。

## <a name="example"></a>示例

下面的示例演示如何指定运行时在何处可以找到程序集。

```xml
<configuration>
   <runtime>
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
         <dependentAssembly>
            <assemblyIdentity name="myAssembly"
                              publicKeyToken="32ab4ba45e0a69a1"
                              culture="neutral" />
            <codeBase version="2.0.0.0"
                      href="http://www.litwareinc.com/myAssembly.dll"/>
         </dependentAssembly>
      </assemblyBinding>
   </runtime>
</configuration>
```

## <a name="see-also"></a>请参阅

- [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)
- [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)
- [指定程序集的位置](../../../../../docs/framework/configure-apps/specify-assembly-location.md)
- [运行时如何定位程序集](../../../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)
