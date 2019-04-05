---
title: <loadFromRemoteSources> 元素
ms.date: 05/24/2018
helpviewer_keywords:
- loadFromRemoteSources element
- <loadFromRemoteSources> element
ms.assetid: 006d1280-2ac3-4db6-a984-a3d4e275046a
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7568129f30267b212737ec8aa688cf882e19bbff
ms.sourcegitcommit: b8ace47d839f943f785b89e2fff8092b0bf8f565
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2019
ms.locfileid: "55675304"
---
# <a name="loadfromremotesources-element"></a>\<loadFromRemoteSources > 元素
指定是否应为从远程源加载的程序集授予完全信任在.NET Framework 4 及更高版本。
  
> [!NOTE]
>  如果你已由于中的 Visual Studio 项目错误列表或生成错误的错误消息定向到这篇文章，请参阅[如何：使用 Visual Studio 中的程序集从 Web](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ee890038(v=vs.100))。  
  
 \<configuration>  
\<运行时 >  
\<loadFromRemoteSources>  
  
## <a name="syntax"></a>语法  
  
```xml  
<loadFromRemoteSources    
   enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`enabled`|必需的特性。<br /><br /> 指定是否应为从远程源加载的程序集授予完全信任。|  
  
## <a name="enabled-attribute"></a>已启用的属性  
  
|值|描述|  
|-----------|-----------------|  
|`false`|不要授予完全信任应用程序从远程源。 这是默认设置。|  
|`true`|从远程源向应用程序授予完全信任。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关运行时初始化选项的信息。|  
  
## <a name="remarks"></a>备注

在.NET Framework 3.5 和更早版本中，如果从远程位置，加载程序集则在程序集中的代码运行时中以部分信任方式取决于从中加载该区域的授予集。 例如，如果从网站加载程序集，它将加载到 Internet 区域，并向其授予 Internet 权限集。 换而言之，它将执行在 Internet 沙箱中。

从.NET Framework 4 开始，已禁用代码访问安全性 (CAS) 策略和程序集被加载到完全信任。 通常，这会向与加载的程序集授予完全信任<xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType>以前曾沙盒的方法。 若要防止此情况，默认情况下禁用从远程源加载的程序集在运行代码的能力。 默认情况下，如果你尝试加载远程程序集，<xref:System.IO.FileLoadException>使用像引发以下异常消息：

```text
System.IO.FileNotFoundException: Could not load file or assembly 'file:assem.dll' or one of its dependencies. Operation is not supported. 
(Exception from HRESULT: 0x80131515)
File name: 'file:assem.dll' ---> 
System.NotSupportedException: An attempt was made to load an assembly from a network location which would have caused the assembly 
to be sandboxed in previous versions of the .NET Framework. This release of the .NET Framework does not enable CAS policy by default, 
so this load may be dangerous. If this load is not intended to sandbox the assembly, please enable the loadFromRemoteSources switch. 
```

若要加载的程序集和执行其代码，您必须：

- 显式程序集创建一个沙盒 (请参阅[如何：运行沙盒中部分受信任的代码](../../../../../docs/framework/misc/how-to-run-partially-trusted-code-in-a-sandbox.md))。

- 在完全信任环境中运行该程序集的代码。 执行此操作通过配置`<loadFromRemoteSources>`元素。 它允许您指定在早期版本的.NET Framework 中的部分信任中运行的程序集现在运行在完全信任环境中的.NET Framework 4 和更高版本。

> [!IMPORTANT]
> 如果该程序集不应在完全信任环境中运行，则不要设置此配置元素。 相反，创建沙盒<xref:System.AppDomain>要在其中加载程序集。

`enabled`属性`<loadFromRemoteSources>`元素仅当禁用代码访问安全性 (CAS) 时才有效。 默认情况下，在.NET Framework 4 和更高版本中禁用 CAS 策略。 如果您设置`enabled`到`true`，远程程序集被授予完全信任。

如果`enabled`未设置为`true`、<xref:System.IO.FileLoadException>引发在以下条件之一：

- 当前域的沙盒行为是不同于.NET Framework 3.5 中其行为。 这要求 CAS 策略才可被禁用，并且不被进行沙箱处理的当前域。

- 正在加载的程序集不是来自`MyComputer`区域。

设置`<loadFromRemoteSources>`元素`true`可防止引发此异常。 它可用于指定，您不依赖于到沙盒公共语言运行时加载的程序集的安全性，和他们可以有权执行在完全信任。

## <a name="notes"></a>说明

- 在.NET Framework 4.5 和更高版本中，本地网络共享上的程序集在完全信任环境中默认情况下运行;无需启用`<loadFromRemoteSources>`元素。

- 如果应用程序是从 Web 复制而来，Windows 会将其标记为 Web 应用程序，即使它驻留在本地计算机上也不例外。 可以通过更改其文件属性，更改该标记也可以使用`<loadFromRemoteSources>`元素对程序集授予完全信任。 对于操作系统标记为从 Web 加载的本地程序集，也可以使用 <xref:System.Reflection.Assembly.UnsafeLoadFrom%2A> 方法进行加载。

- 你可能会收到<xref:System.IO.FileLoadException>Windows Virtual PC 应用程序中运行的应用程序中。 当你尝试从托管计算机上的链接文件夹加载文件时，可以发生这种情况。 当你尝试将文件从上链接的文件夹加载它也会发生[远程桌面服务](https://go.microsoft.com/fwlink/?LinkId=182775)(Terminal Services)。 若要避免此异常，设置`enabled`到`true`。

## <a name="configuration-file"></a>配置文件

此元素通常用在应用程序配置文件中，但可根据上下文用于其他配置文件。 有关详细信息，请参阅文章[多个隐式使用 CAS 策略： loadFromRemoteSources](https://go.microsoft.com/fwlink/p/?LinkId=266839) .NET 安全性博客中。  

## <a name="example"></a>示例

下面的示例演示如何向从远程源加载的程序集授予完全信任。

```xml
<configuration>  
   <runtime>  
      <loadFromRemoteSources enabled="true"/>  
   </runtime>  
</configuration>  
```

## <a name="see-also"></a>请参阅

- [更多隐式使用 CAS 策略： loadFromRemoteSources](https://go.microsoft.com/fwlink/p/?LinkId=266839)
- [如何：运行沙盒中部分受信任的代码](../../../../../docs/framework/misc/how-to-run-partially-trusted-code-in-a-sandbox.md)
- [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)
- [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)
- <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType>
