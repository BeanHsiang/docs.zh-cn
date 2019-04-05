---
title: 如何：验证应用程序设置
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- validating application settings
- application settings [Windows Forms], Windows Forms
- application settings [Windows Forms], validating
ms.assetid: 9f145ada-4267-436a-aa4c-c4dcffd0afb7
ms.openlocfilehash: 96323e0edd643e20338bd10a9eb1744c3b0aef2f
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57705826"
---
# <a name="how-to-validate-application-settings"></a>如何：验证应用程序设置
本主题演示如何在保留应用程序设置前先验证它们。  
  
 由于应用程序设置是强类型设置，因此在一定程度上可以相信用户无法向给定设置分配错误类型的数据。 但是，用户仍有可能尝试向设置分配超出可接受范围的值，例如，用户提供的出生日期可能是一个将来日期。 <xref:System.Configuration.ApplicationSettingsBase>所有应用程序设置类的父类公开四个事件，若要启用此类边界检查。 处理这些事件会将所有验证代码放置在同一位置中，而不是将其分散到整个项目。  
  
 所用事件取决于需要何时验证设置，如下表所述。  
  
|事件|发生时间和用法|  
|-----------|------------------------|  
|<xref:System.Configuration.ApplicationSettingsBase.SettingsLoaded>|初始加载设置属性组后发生。<br /><br /> 在应用程序中使用属性组前，使用此事件验证整个属性组的初始值。|  
|<xref:System.Configuration.ApplicationSettingsBase.SettingChanging>|在更改单个设置属性的值之前发生。<br /><br /> 更改单个属性之前，使用此事件验证该属性。 它可以向用户提供有关其操作和选择的即时反馈。|  
|<xref:System.Configuration.ApplicationSettingsBase.PropertyChanged>|在更改单个设置属性的值之后发生。<br /><br /> 更改单个属性之后，使用此事件验证该属性。 除非需要进行长时间的异步验证处理，否则很少将此事件用于验证操作。|  
|<xref:System.Configuration.ApplicationSettingsBase.SettingsSaving>|在存储设置属性组之前发生。<br /><br /> 将属性组保留到磁盘之前，使用此事件验证整个属性组的值。|  
  
 通常，不会在同一应用程序中使用所有这些事件进行验证操作。 例如，则通常可以通过仅处理满足所有验证需求<xref:System.Configuration.ApplicationSettingsBase.SettingChanging>事件。  
  
 事件处理程序检测到无效值时通常执行以下操作之一：  
  
-   自动提供已知是正确的值，如默认值。  
  
-   再次询问服务器代码用户，以获取信息。  
  
-   如及其关联的操作之前引发的事件<xref:System.Configuration.ApplicationSettingsBase.SettingChanging>并<xref:System.Configuration.ApplicationSettingsBase.SettingsSaving>，使用<xref:System.ComponentModel.CancelEventArgs>参数来取消该操作。  
  
 有关事件处理的详细信息，请参阅[事件处理程序概述](../event-handlers-overview-windows-forms.md)。  
  
 以下过程介绍如何测试使用的有效的出生日期<xref:System.Configuration.ApplicationSettingsBase.SettingChanging>或<xref:System.Configuration.ApplicationSettingsBase.SettingsSaving>事件。 这些过程是在假定已创建应用程序设置的情况下编写的；在此示例中，我们将对名为 `DateOfBirth` 的设置执行边界检查。 有关创建设置的详细信息，请参阅[如何：创建应用程序设置](how-to-create-application-settings.md)。  
  
### <a name="to-obtain-the-application-settings-object"></a>获取应用程序设置对象  
  
-   通过完成以下项目符号项之一，获取对应用程序设置对象（包装器实例）的引用：  
  
    -   如果使用“属性编辑器”中的“Visual Studio 应用程序设置”对话框创建设置，则可通过以下表达式检索为语言生成的默认设置对象。  
  
        ```csharp  
        Configuration.Settings.Default   
        ```  
  
        ```vb  
        MySettings.Default   
        ```  
  
         或  
  
    -   如果是 Visual Basic 开发人员并使用项目设计器创建应用程序设置，则可通过使用 [My.Settings Object](~/docs/visual-basic/language-reference/objects/my-settings-object.md) 对象来检索设置。  
  
         或  
  
    -   如果通过从派生来创建你的设置<xref:System.Configuration.ApplicationSettingsBase>直接，您需要手动实例化类。  
  
        ```csharp  
        MyCustomSettings settings = new MyCustomSettings();  
        ```  
  
        ```vb  
        Dim Settings as New MyCustomSettings()  
        ```  
  
 下列过程的编写依据：假定应用程序设置对象是通过完成本过程中最后一个项目符号项来获取的。  
  
### <a name="to-validate-application-settings-when-a-setting-is-changing"></a>设置更改时验证应用程序设置  
  
1.  如果您是C#开发人员，在窗体或控件的`Load`事件添加事件处理程序<xref:System.Configuration.ApplicationSettingsBase.SettingChanging>事件。  
  
     或  
  
     如果是 Visual Basic 开发人员，则应使用 `WithEvents` 关键字声明 `Settings` 变量。  
  
    ```csharp  
    public void Form1_Load(Object sender, EventArgs e)   
    {  
        settings.SettingChanging += new SettingChangingEventHandler(MyCustomSettings_SettingChanging);  
    }  
    ```  
  
    ```vb  
    Public Sub Form1_Load(sender as Object, e as EventArgs)  
        AddHandler settings.SettingChanging, AddressOf MyCustomSettings_SettingChanging  
    End Sub   
    ```  
  
2.  定义事件处理程序，并在该事件处理程序中编写代码，以便对出生日期执行边界检查。  
  
    ```csharp  
    private void MyCustomSettings_SettingChanging(Object sender, SettingChangingEventArgs e)  
    {  
        if (e.SettingName.Equals("DateOfBirth")) {  
            Date newDate = (Date)e.NewValue;  
            If (newDate > Date.Now) {  
                e.Cancel = true;  
                // Inform the user.  
            }  
        }  
    }  
    ```  
  
    ```vb  
    Private Sub MyCustomSettings_SettingChanging(sender as Object, e as SettingChangingEventArgs) Handles Settings.SettingChanging  
        If (e.SettingName.Equals("DateOfBirth")) Then  
            Dim NewDate as Date = CType(e.NewValue, Date)  
            If (NewDate > Date.Now) Then  
                e.Cancel = True  
                ' Inform the user.  
            End If  
        End If  
    End Sub  
    ```  
  
### <a name="to-validate-application-settings-when-a-save-occurs"></a>保存时验证应用程序设置  
  
1.  在窗体或控件的`Load`事件，添加的事件处理程序<xref:System.Configuration.ApplicationSettingsBase.SettingsSaving>事件。  
  
    ```csharp  
    public void Form1_Load(Object sender, EventArgs e)   
    {  
        settings.SettingsSaving += new SettingsSavingEventHandler(MyCustomSettings_SettingsSaving);  
    }  
    ```  
  
    ```vb  
    Public Sub Form1_Load(Sender as Object, e as EventArgs)  
        AddHandler settings.SettingsSaving, AddressOf MyCustomSettings_SettingsSaving  
    End Sub  
    ```  
  
2.  定义事件处理程序，并在该事件处理程序中编写代码，以便对出生日期执行边界检查。  
  
    ```csharp  
    private void MyCustomSettings_SettingsSaving(Object sender, SettingsSavingEventArgs e)  
    {  
        if (this["DateOfBirth"] > Date.Now) {  
            e.Cancel = true;  
        }  
    }  
    ```  
  
    ```vb  
    Private Sub MyCustomSettings_SettingsSaving(Sender as Object, e as SettingsSavingEventArgs)  
        If (Me["DateOfBirth"] > Date.Now) Then  
            e.Cancel = True  
        End If  
    End Sub  
    ```  
  
## <a name="see-also"></a>请参阅
- [在 Windows 窗体中创建事件处理程序](../creating-event-handlers-in-windows-forms.md)
- [如何：创建应用程序设置](how-to-create-application-settings.md)
