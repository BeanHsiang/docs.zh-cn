---
title: <appSettings> 的 <configuration> 元素
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/appSettings
helpviewer_keywords:
- appSettings Element
- <appSettings> Element
ms.assetid: 39694cc4-6b84-45a6-9329-385a0d8b48fe
author: guardrex
ms.author: mairaw
ms.openlocfilehash: dcdf8d0f11ae65353da08bba1f8d2fe5ab415c6b
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55289583"
---
# <a name="appsettings-element-for-configuration"></a>\<appSettings > 元素\<配置 >

包含自定义应用程序设置。 这是.NET Framework 提供的预定义的配置部分。

[**\<configuration>**](~/docs/framework/configure-apps/file-schema/configuration-element.md)   
&nbsp;&nbsp;**\<appSettings>**

## <a name="syntax"></a>语法

```xml
<appSettings>
  <!-- Elements to add, clear, or remove configuration settings -->
</appSettings>
```

## <a name="attribute"></a>特性

|           | 描述 |
| --------- | ----------- |
| 文件  | 可选特性。<br><br>指定包含自定义应用程序配置设置的外部文件的相对路径。 指定的文件是否包含相同类型的设置中指定 **\<添加 >** ， **\<删除 >**，以及 **\<清除 >** 元素，并使用同一个键/值对的格式设置为这些元素。<br><br>指定的路径是相对于主配置文件。 对于 Windows 窗体应用程序，这是二进制文件夹 (如 */bin/debug*)，不应用程序配置文件的位置。 为 Web 窗体应用程序的路径是相对于应用程序根目录中，其中*web.config*文件的位置。<br><br>请注意，运行时会忽略该属性，是否找不到指定的文件。 |

## <a name="parent-element"></a>父元素

|     | 描述 |
| --- | ----------- |
| [**\<配置 >** 元素](~/docs/framework/configure-apps/file-schema/configuration-element.md) | 公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。 |

## <a name="child-elements"></a>子元素

|     | 描述 |
| --- | ----------- |
| [**\<add>**](~/docs/framework/configure-apps/file-schema/appsettings/add-element-for-appsettings.md) | 添加自定义应用程序设置。 |
| [**\<clear>**](~/docs/framework/configure-apps/file-schema/appsettings/clear-element-for-appsettings.md) | 清除所有以前定义的应用程序设置。 |
| [**\<remove>**](~/docs/framework/configure-apps/file-schema/appsettings/remove-element-for-appsettings.md) | 删除以前定义的应用程序设置。 |

## <a name="remarks"></a>备注

**\<AppSettings >** 元素将自定义应用程序配置信息，如数据库连接字符串、 文件路径、 XML Web service Url 或任何其他自定义配置信息存储应用程序。 中指定的键/值对 **\<appSettings >** 在代码中使用访问元素<xref:System.Configuration.ConfigurationSettings>类。

可以使用**文件**属性中 **\<appSettings >** 元素的*Web.config*和应用程序配置文件。 此属性指定提供其他设置或重写中指定的设置的配置文件 **\<appSettings >** 元素。 **文件**属性可以在源代码管理团队开发方案，例如当用户需要重写应用程序配置文件中指定的项目设置中使用。

指定的配置文件 **文件** 属性必须具有的根节点 **\<appSettings >** 而非 **\<配置 >**.

## <a name="example"></a>示例

下面的示例演示外部应用程序设置文件 (custom.config)，该文件定义自定义应用程序设置：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<appSettings>
  <add key="MyCustomSetting" value="MyCustomSettingValue" />
</appSettings>
```

下面的示例演示使用外部设置文件中的设置并自行设置应用程序设置的应用程序配置文件：

```xml
<configuration>
  <appSettings file="custom.config">
    <add key="ApplicationName" value="MyApplication" />
  </appSettings>
</configuration>
```

## <a name="configuration-file"></a>配置文件

在应用程序配置文件中，计算机配置文件可以使用此元素 (*Machine.config*)，并*Web.config*不在应用程序目录级别上的文件。

## <a name="see-also"></a>请参阅

- [.NET Framework 的配置文件架构](~/docs/framework/configure-apps/file-schema/index.md)
