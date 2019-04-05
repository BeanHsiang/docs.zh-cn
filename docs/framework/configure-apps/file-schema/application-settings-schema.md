---
title: 应用程序设置架构
ms.date: 03/30/2017
helpviewer_keywords:
- schema application settings
- application settings, schema [Windows Forms]
- Windows Forms, application settings schema
- configuration schema [.NET Framework], application settings
ms.assetid: 5797fcff-6081-4e8c-bebf-63d9c70cf14b
ms.openlocfilehash: a74716bcdf3c85c08d0ff3bf66407dce30ee91cc
ms.sourcegitcommit: b351b0781a035616c90c68ccae6dd60aae66a953
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2019
ms.locfileid: "55083465"
---
# <a name="application-settings-schema"></a>应用程序设置架构

应用程序设置允许 Windows 窗体或 ASP.NET 应用程序来存储和检索应用程序范围和用户范围的设置。 在此上下文中，*设置*是任何可能是特定于应用程序或特定于当前用户的信息 — 从用户的数据库连接字符串的任何内容的首选默认窗口大小。

默认情况下，应用程序设置 Windows 窗体应用程序中的使用<xref:System.Configuration.LocalFileSettingsProvider>类，该类使用.NET 配置系统来存储在 XML 配置文件中的设置。 有关使用应用程序设置的文件的详细信息，请参阅[应用程序设置体系结构](~/docs/framework/winforms/advanced/application-settings-architecture.md)。

应用程序设置定义了以下元素，它使用的配置文件的一部分。

| 元素                    | 描述                                                                           |
| -------------------------- | ------------------------------------------------------------------------------------- |
| **\<applicationSettings>** | 包含所有**\<设置 >** 标记特定于应用程序。                         |
| **\<userSettings>**        | 包含所有**\<设置 >** 特定于当前用户的标记。                        |
| **\<setting>**             | 定义设置。 子 **\<applicationSettings >** 或 **\<userSettings >**。 |
| **\<value>**               | 定义设置的值。 子级**\<设置 >**。                                   |

## <a name="applicationsettings-element"></a>\<applicationSettings > 元素

此元素包含所有**\<设置 >** 特定于客户端计算机上的应用程序的实例的标记。 未定义任何属性。

## <a name="usersettings-element"></a>\<用户设置 > 元素

此元素包含所有**\<设置 >** 特定于当前正在使用该应用程序的用户的标记。 未定义任何属性。

## <a name="setting-element"></a>\<设置 > 元素

此元素定义设置。 它具有以下属性。

| 特性        | 描述 |
| ---------------- | ----------- |
| **name**         | 必需。 设置的唯一 ID。 通过 Visual Studio 创建的设置保存名称`ProjectName.Properties.Settings`。 |
| **serializedAs** | 必需。 要用来序列化的值为文本的格式。 有效值为：<br><br>- `string`. 值序列化为字符串使用<xref:System.ComponentModel.TypeConverter>。<br>- `xml`. 使用 XML 序列化序列化值。<br>- `binary`. 值序列化为文本编码的二进制文件使用二进制序列化。<br />- `custom`. 设置提供程序具有此设置的固有知识和序列化和反序列化。 |

## <a name="value-element"></a>\<值 > 元素

此元素包含设置的值。

## <a name="example"></a>示例

下面的示例演示定义了两个应用程序范围设置和两个用户范围设置的应用程序设置文件：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
    <sectionGroup name="applicationSettings" type="System.Configuration.ApplicationSettingsGroup, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">
      <section name="WindowsApplication1.Properties.Settings" type="System.Configuration.ClientSettingsSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
    </sectionGroup>
    <sectionGroup name="userSettings" type="System.Configuration.UserSettingsGroup, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">
      <section name="WindowsApplication1.Properties.Settings" type="System.Configuration.ClientSettingsSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" allowExeDefinition="MachineToLocalUser" />
    </sectionGroup>
  </configSections>
  <applicationSettings>
    <WindowsApplication1.Properties.Settings>
      <setting name="Cursor" serializeAs="String">
        <value>Default</value>
      </setting>
      <setting name="DoubleBuffering" serializeAs="String">
        <value>False</value>
      </setting>
    </WindowsApplication1.Properties.Settings>
  </applicationSettings>
  <userSettings>
    <WindowsApplication1.Properties.Settings>
      <setting name="FormTitle" serializeAs="String">
        <value>Form1</value>
      </setting>
      <setting name="FormSize" serializeAs="String">
        <value>595, 536</value>
      </setting>
    </WindowsApplication1.Properties.Settings>
  </userSettings>
</configuration>
```

## <a name="see-also"></a>请参阅

- [应用程序设置概述](~/docs/framework/winforms/advanced/application-settings-overview.md)
- [应用程序设置体系结构](~/docs/framework/winforms/advanced/application-settings-architecture.md)
