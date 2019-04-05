---
title: <configuration> 元素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration
helpviewer_keywords:
- <configuration> element
- configuration element
- container tags, <configuration> element
ms.assetid: 2ec1c9dc-2e5c-4ef0-9958-81670ab88449
ms.openlocfilehash: 9a7b25c74763c020c0e19c3f6099db9001acf773
ms.sourcegitcommit: b8ace47d839f943f785b89e2fff8092b0bf8f565
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2019
ms.locfileid: "55675044"
---
# <a name="configuration-element"></a>\<配置 > 元素

公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。

**\<configuration>**

## <a name="syntax"></a>语法

```xml
<configuration>
  <!-- Configuration settings -->
</configuration>
```

## <a name="attributes"></a>特性

无

## <a name="parent-element"></a>父元素

无

## <a name="child-elements"></a>子元素

|     | 描述 |
| --- | ----------- |
| [**\<assemblyBinding>**](~/docs/framework/configure-apps/file-schema/assemblybinding-element-for-configuration.md) | 指定配置级的程序集绑定策略。|
| [**\<启动 >** 设置架构](~/docs/framework/configure-apps/file-schema/startup/index.md) | 启动设置架构中的所有元素。 |
| [**\<运行时 >** 设置架构](~/docs/framework/configure-apps/file-schema/runtime/index.md) | 在运行时设置架构中的所有元素。 |
| [**\<system.runtime.remoting >** 设置架构](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/z415cf9a(v=vs.100)) | 远程处理设置架构中的所有元素。 |
| [**\<system.Net >** 设置架构](~/docs/framework/configure-apps/file-schema/network/index.md) | 网络设置架构中的所有元素。 |
| [**\<cryptographySettings >** 设置架构](~/docs/framework/configure-apps/file-schema/cryptography/index.md) | 加密设置架构中的所有元素。 |
| [**\<配置 >** 节架构](~/docs/framework/configure-apps/file-schema/configuration-sections-schema.md) | 配置部分设置架构中的所有元素。 |
| [跟踪和调试设置架构](~/docs/framework/configure-apps/file-schema/trace-debug/index.md) | 跟踪和调试设置架构中的所有元素。 |
| [ASP.NET 配置设置架构](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/b5ysx397(v=vs.100)) | 在 ASP.NET 配置架构中，其中包括用于配置 ASP.NET 网站和应用程序的元素的所有元素。 在中使用*Web.config*文件。 |
| [**\<webServices>** Settings Schema](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cctwteet(v=vs.100)) | Web 服务设置架构中的所有元素。 |
| [Web 设置架构](~/docs/framework/configure-apps/file-schema/web/index.md) | Web 设置架构中的所有元素，包括用于配置 ASP.NET 如何与主机应用程序（如 IIS）一起工作的元素。 在中使用*aspnet.config*文件。 |

## <a name="remarks"></a>备注

每个配置文件必须包含一个**\<配置 >** 元素。

## <a name="see-also"></a>请参阅

- [.NET Framework 的配置文件架构](~/docs/framework/configure-apps/file-schema/index.md)
