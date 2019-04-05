---
title: <section> 元素
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/configSections/section
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/configSections/sectionGroup/section
helpviewer_keywords:
- section Element
- <section> Element
ms.assetid: ec7d4110-2403-47ac-8218-499bfe9d5ddb
author: guardrex
ms.author: mairaw
ms.openlocfilehash: 58f823ce0c128f30e361b4a631d41286533b5f0f
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55259210"
---
# <a name="section-element"></a>\<部分 > 元素

包含配置部分声明。

[**\<configuration>**](~/docs/framework/configure-apps/file-schema/configuration-element.md)   
&nbsp;&nbsp;[**\<configSections>**](~/docs/framework/configure-apps/file-schema/configsections-element-for-configuration.md)   
&nbsp;&nbsp;&nbsp;&nbsp;**\<section>**

[**\<configuration>**](~/docs/framework/configure-apps/file-schema/configuration-element.md)   
&nbsp;&nbsp;[**\<configSections>**](~/docs/framework/configure-apps/file-schema/configsections-element-for-configuration.md)   
&nbsp;&nbsp;&nbsp;&nbsp;[**\<sectionGroup>**](~/docs/framework/configure-apps/file-schema/sectiongroup-element-for-configsections.md)   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<section>**

## <a name="syntax"></a>语法

```xml
<section name="section name"
         type="configuration section handler class, assembly"
         allowDefinition="Everywhere|MachineOnly|MachineToApplication" 
         allowLocation="true|false" />
```

## <a name="required-attributes"></a>必需的特性

|           | 描述 |
| --------- | ----------- |
| **name**  | 指定配置节的名称。 |
| **type**  | 指定从配置文件中读取部分的配置节处理程序类的名称。 类型值具有语法"fully-qualified-section-handler-class-name，简单的程序集名称"。 简单的程序集名称是根文件名而不 *.dll*文件扩展名。 |

## <a name="optional-attributes"></a>可选属性

以下属性是仅适用于 ASP.NET 应用程序。 配置系统将忽略这些属性对于其他应用程序类型。

|                     | 描述 |
| ------------------- | ----------- |
| **allowDefinition** | 指定部分可在哪个配置文件。 使用下列值之一：<br><br>**Everywhere**<br>允许使用任何配置文件中的部分。 这是默认设置。<br>**MachineOnly**<br>允许该节只能在计算机配置文件 (*Machine.config*)。<br>**MachineToApplication**<br>允许要在计算机配置文件或应用程序配置文件中使用的部分。 |
| **allowLocation**   | 确定是否可以在使用部分**\<位置 >** 元素。 使用下列值之一：<br><br>**true**<br>允许该节中使用**\<位置 >** 元素。 这是默认设置。<br>**false**<br>不允许要在中使用的部分**\<位置 >** 元素。 |

## <a name="parent-elements"></a>父元素

|     | 描述 |
| --- | ----------- |
| [**\<configSections >** 元素](~/docs/framework/configure-apps/file-schema/configsections-element-for-configuration.md) | 包含配置节和命名空间声明。 |
| [**\<sectionGroup>** Element](~/docs/framework/configure-apps/file-schema/sectiongroup-element-for-configsections.md) | 定义配置节的命名空间。 |

> [!NOTE]
> 一个**\<部分 >** 元素是子元素的 **\<configSections >** 或者 **\<sectionGroup >** 但不是两者。

## <a name="child-elements"></a>子元素

无

## <a name="remarks"></a>备注

实质上声明一个配置节定义配置文件的新元素。 新元素包含一个配置节处理程序的设置 (即，实现的类<xref:System.Configuration.IConfigurationSectionHandler>接口) 读取。 属性和子元素的定义的部分取决于用于读取您的设置的节处理程序。

声明中的配置节处理程序*Machine.config*文件，您可以在该计算机上的任何应用程序配置文件中使用的配置节除非**allowDefinition**属性另行指定。

## <a name="example"></a>示例

下面的示例演示如何定义配置节和定义该部分的设置：

```xml
<configuration>
  <configSections>
    <section name="sampleSection"
             type="System.Configuration.SingleTagSectionHandler" 
             allowLocation="false" />
  </configSections>
  <sampleSection setting1="Value1" 
                 setting2="value two" 
                 setting3="third value" />
</configuration>
```

## <a name="configuration-file"></a>配置文件

在应用程序配置文件中，计算机配置文件可以使用此元素 (*Machine.config*)，并*Web.config*不在应用程序目录级别上的文件。

## <a name="see-also"></a>请参阅

- [.NET Framework 的配置文件架构](~/docs/framework/configure-apps/file-schema/index.md)
