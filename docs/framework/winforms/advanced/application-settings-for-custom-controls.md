---
title: 自定义控件的应用程序设置
ms.date: 03/30/2017
helpviewer_keywords:
- custom controls [Windows Forms], application settings
- application settings [Windows Forms], custom controls
ms.assetid: f44afb74-76cc-44f2-890a-44b7cdc211a1
ms.openlocfilehash: d12caf9ed2cb80d837080badab436b2e9b0b3728
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57714341"
---
# <a name="application-settings-for-custom-controls"></a>自定义控件的应用程序设置
必须完成某些任务，以使能够保持应用程序设置时的控件都承载在第三方应用程序中的自定义控件。  
  
 表示正在创建独立的应用程序假设下编写大部分的应用程序设置功能有关的文档。 但是，如果要在其应用程序中创建其他开发人员将承载的控件，您需要执行几个额外的步骤为您的控件保存其设置正确。  
  
## <a name="application-settings-and-custom-controls"></a>应用程序设置和自定义控件  
 为能够正确地保持其设置控件，它必须通过创建自己专用的应用程序设置包装类，派生自封装过程<xref:System.Configuration.ApplicationSettingsBase>。 此外，主控件类必须实现<xref:System.Configuration.IPersistComponentSettings>。 此接口包含多个属性，以及两个方法，<xref:System.Configuration.IPersistComponentSettings.LoadComponentSettings%2A>和<xref:System.Configuration.IPersistComponentSettings.SaveComponentSettings%2A>。 如果将控件添加到窗体使用**Windows 窗体设计器**在 Visual Studio 中，将调用 Windows 窗体<xref:System.Configuration.IPersistComponentSettings.LoadComponentSettings%2A>自动在初始化该控件时，必须调用<xref:System.Configuration.IPersistComponentSettings.SaveComponentSettings%2A>您在`Dispose`控件的方法。  
  
 此外，应为应用程序设置以便在设计时环境，如 Visual Studio 中正常工作的自定义控件来实现以下：  
  
1.  具有采用的构造函数的自定义应用程序设置类<xref:System.ComponentModel.IComponent>作为单个参数。 使用此类来保存和加载的所有应用程序设置。 当创建此类的新实例时，请传递自定义控件使用的构造函数。  
  
2.  创建控件并将其放置在窗体，如在窗体的后创建此自定义设置类<xref:System.Windows.Forms.Form.Load>事件处理程序。  
  
 有关创建自定义设置类的说明，请参阅[如何：创建应用程序设置](how-to-create-application-settings.md)。  
  
## <a name="settings-keys-and-shared-settings"></a>设置密钥和共享的设置  
 某些控件可以在同一个窗体中多次使用。 大多数情况下，将需要这些控件，以持久保存其自己单独的设置。 与<xref:System.Configuration.IPersistComponentSettings.SettingsKey%2A>属性上的<xref:System.Configuration.IPersistComponentSettings>，可以提供以区分多个版本的窗体上控件的唯一字符串。  
  
 最简单的方法实现<xref:System.Configuration.IPersistComponentSettings.SettingsKey%2A>是使用<xref:System.Windows.Forms.Control.Name%2A>的控件属性<xref:System.Configuration.IPersistComponentSettings.SettingsKey%2A>。 当加载或保存控件的设置时，您传递的值<xref:System.Configuration.IPersistComponentSettings.SettingsKey%2A>到<xref:System.Configuration.ApplicationSettingsBase.SettingsKey%2A>属性的<xref:System.Configuration.ApplicationSettingsBase>类。 它将用户的设置保存到 XML 时，应用程序设置将使用此唯一键。 下面的代码示例演示如何`<userSettings>`部分中的名为的自定义控件的实例可能看起来`CustomControl1`，它将保存的设置其`Text`属性。  
  
```xml  
<userSettings>  
    <CustomControl1>  
        <setting name="Text" serializedAs="string">  
            <value>Hello, World</value>  
        </setting>  
    </CustomControl1>  
</userSettings>  
```  
  
 未提供的值的控件的任何实例<xref:System.Configuration.ApplicationSettingsBase.SettingsKey%2A>将共享相同的设置。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Configuration.ApplicationSettingsBase>
- <xref:System.Configuration.IPersistComponentSettings>
- [应用程序设置体系结构](application-settings-architecture.md)
