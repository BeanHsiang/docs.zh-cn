---
title: 指定程序集的位置
ms.date: 03/30/2017
helpviewer_keywords:
- configuration [.NET Framework], applications
- application configuration [.NET Framework]
- assemblies [.NET Framework], specifying location
ms.assetid: 1cb92bd7-6bab-44cf-8fd3-36303ce84fea
ms.openlocfilehash: 328fe08872a2b57d0bdf87ea9be9224795ca9ad9
ms.sourcegitcommit: 3500c4845f96a91a438a02ef2c6b4eef45a5e2af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/07/2019
ms.locfileid: "55825402"
---
# <a name="specifying-an-assemblys-location"></a>指定程序集的位置
有两种方法来指定程序集的位置：  
  
-   使用[ \<b a s e >](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md)元素。  
  
-   使用[\<探测 >](../../../docs/framework/configure-apps/file-schema/runtime/probing-element.md)元素。  
  
 此外可以使用[.NET Framework 配置工具 (Mscorcfg.msc)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/2bc0cxhc(v=vs.100))来指定程序集的位置或指定公共语言运行时来探测程序集的位置。  
  
## <a name="using-the-codebase-element"></a>使用\<b a s e > 元素  
 可以使用 **\<b a s e >** 只能机配置或发布服务器策略在文件中还将程序集版本重定向的元素。 当运行时确定要使用的程序集版本时，则会应用确定版本的文件的基本代码设置。 如果指示没有基本代码，运行时探测程序集以正常方式。 有关详细信息，请参阅[运行时如何定位程序集](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)。  
  
 下面的示例演示如何指定程序集的位置。  
  
```xml  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
       <dependentAssembly>  
         <assemblyIdentity name="myAssembly"  
                           publicKeyToken="32ab4ba45e0a69a1"  
                           culture="en-us" />  
         <codeBase version="2.0.0.0"  
                   href="http://www.litwareinc.com/myAssembly.dll"/>  
       </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
 **版本**属性是必需的所有强名称的程序集，但不是具有强名称的程序集，应省略。  **\<B a s e >** 元素需要**href**属性。 不能指定版本范围 **\<b a s e >** 元素。  
  
> [!NOTE]
>  如果你所提供的不是强名称的程序集的基本代码的提示，提示必须指向应用程序基控件或应用程序基目录的子目录。  
  
## <a name="using-the-probing-element"></a>使用\<探测 > 元素  
 运行时定位程序集不具有通过探测的基本代码。 探测的详细信息，请参阅[运行时如何定位程序集](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)。  
  
 可以使用[\<探测 >](../../../docs/framework/configure-apps/file-schema/runtime/probing-element.md)应用程序配置文件来指定运行时查找程序集时应搜索的子目录中的元素。 下面的示例演示如何指定运行时应搜索的目录。  
  
```xml  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <probing privatePath="bin;bin2\subbin;bin3"/>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
 **PrivatePath**属性包含运行时应搜索程序集的目录。 如果应用程序位于 C:\Program Files\MyApp，运行时将查找 C:\Program Files\MyApp\Bin、 C:\Program Files\MyApp\Bin2\Subbin 和 C:\Program Files\MyApp\Bin3 中未指定基本代码的程序集。 中指定的目录**privatePath**必须是应用程序基目录的子目录。  
  
## <a name="see-also"></a>请参阅
- [Assemblies in the Common Language Runtime](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md)（公共语言运行时中的程序集）
- [使用程序集编程](../../../docs/framework/app-domains/programming-with-assemblies.md)
- [运行时如何定位程序集](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)
- [使用配置文件配置应用程序](index.md)
