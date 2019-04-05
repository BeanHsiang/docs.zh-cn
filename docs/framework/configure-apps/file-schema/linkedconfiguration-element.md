---
title: <linkedConfiguration> 元素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/assemblyBinding/linkedConfiguration
- http://schemas.microsoft.com/.NetConfiguration/v2.0#linkedConfiguration
helpviewer_keywords:
- configuration files [.NET Framework],linked configuration files
- <linkedConfiguration> element
- including configuration files
- linked configuration files
- linkedConfiguration Element
ms.assetid: 8eb34f3b-427e-4288-a7ff-c73f489deb45
ms.openlocfilehash: 909ee7cbb7cd31cf213f305b23237cb69e295882
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55284601"
---
# <a name="linkedconfiguration-element"></a>\<linkedConfiguration > 元素

指定要包含的配置文件。

[**\<configuration>**](~/docs/framework/configure-apps/file-schema/configuration-element.md)   
&nbsp;&nbsp;[**\<assemblyBinding>**](~/docs/framework/configure-apps/file-schema/assemblybinding-element-for-configuration.md)   
&nbsp;&nbsp;&nbsp;&nbsp;**\<linkedConfiguration>**

## <a name="syntax"></a>语法

```xml
<linkedConfiguration href="URL of linked configuration file" />
```

## <a name="attribute"></a>特性

|           | 描述 |
| --------- | ----------- |
| **href**  | 必需的特性。<br><br>要包括在配置文件的 URL。 有关支持的唯一格式**href**属性是`file://`。 支持本地文件和 UNC 文件。 |

## <a name="parent-element"></a>父元素

|     | 描述 |
| --- | ----------- |
| [**\<assemblyBinding >** 元素](~/docs/framework/configure-apps/file-schema/assemblybinding-element-for-configuration.md) | 指定配置级的程序集绑定策略。 |

## <a name="child-elements"></a>子元素

无

## <a name="remarks"></a>备注

 **\<LinkedConfiguration >** 元素可简化维护组件程序集。 如果一个或多个应用程序使用的程序集都驻留在已知位置中的配置文件，可以使用的应用程序使用的程序集的配置文件 **\<linkedConfiguration >** 若要包括程序集配置文件，而不是直接包含配置信息的元素。 组件程序集已维修，更新常见的配置文件提供所有应用程序使用的程序集的更新的配置的信息。

> [!NOTE]
>  **\<LinkedConfiguration >** 元素不支持使用 Windows 通过并行清单的应用程序。

链接的配置文件的使用遵循以下规则：

- 包含的配置文件中设置只会影响加载程序绑定策略，并且仅由加载程序。 包含的配置文件可以具有设置不是绑定策略，但这些设置不产生任何影响。

- 有关支持的唯一格式`href`属性是`file://`。 支持本地文件和 UNC 文件。

- 没有任何约束的每个配置文件的链接配置数量上。

- 所有链接的配置文件经过合并以形成一个文件的行为类似`#include`C/c + + 中的指令。

-  **\<LinkedConfiguration >** 元素允许仅在应用程序配置文件中; 在将被忽略*Machine.config*。

- 检测到并终止循环引用。 也就是说，如果 **\<linkedConfiguration >** 一系列配置文件中的元素形成循环，循环将检测并停止。

## <a name="example"></a>示例

下面的示例演示如何包含配置文件从本地硬盘：

```xml
<configuration>
  <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
    <linkedConfiguration href="file://c:\Program Files\Contoso\sharedConfig.xml"/>
  </assemblyBinding>
</configuration>
```

## <a name="see-also"></a>请参阅

- [**\<assemblyBinding >** 元素](~/docs/framework/configure-apps/file-schema/assemblybinding-element-for-configuration.md)
- [.NET Framework 的配置文件架构](~/docs/framework/configure-apps/file-schema/index.md)
