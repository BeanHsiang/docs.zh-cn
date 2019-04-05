---
title: 在 Windows 窗体中的高 DPI 支持
ms.date: 05/16/2017
helpviewer_keywords:
- High DPI in Windows Forms
- Dynamic rescaling in Windows Forms
- Windows Forms layout
- Windows Forms dynamic resizing
ms.assetid: 075ea4c3-900c-4f8a-9dd2-13ea6804346b
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1641702c7b1c3d3b0e83c59a96529de70f699d17
ms.sourcegitcommit: 69bf8b719d4c289eec7b45336d0b933dd7927841
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/14/2019
ms.locfileid: "57843604"
---
# <a name="high-dpi-support-in-windows-forms"></a>在 Windows 窗体中的高 DPI 支持

从.NET Framework 4.7 开始，Windows 窗体包括增强功能的常见高 DPI 和动态 DPI 方案。 这些问题包括：

- 改进的缩放和多个 Windows 窗体的布局控件，如<xref:System.Windows.Forms.MonthCalendar>控件和<xref:System.Windows.Forms.CheckedListBox>控件。

- 单次传递缩放。  在.NET Framework 4.6 和更早版本中，通过多个通过，这导致一些控件，以扩展超过需要执行缩放。

- 对 Windows 窗体应用程序已启动后在用户更改 DPI 或缩放系数的动态 DPI 方案的支持。

在版本的.NET Framework 从.NET Framework 4.7 开始，增强了高 DPI 支持是可选功能。 必须配置应用程序以充分利用它。

## <a name="configuring-your-windows-forms-app-for-high-dpi-support"></a>高 DPI 支持在 Windows 窗体应用中配置

支持高 DPI 识别的新 Windows 窗体功能是仅在面向.NET Framework 4.7 和从 Windows 10 创意者更新的 Windows 操作系统上运行的应用程序中可用。

此外，若要在 Windows 窗体应用程序中配置高 DPI 支持，必须执行以下操作：

- 声明与 Windows 10 的兼容性。

  若要执行此操作，以下代码添加到清单文件：

  ```xml
  <compatibility xmlns="urn:schemas-microsoft-com:compatibility.v1">
    <application>
      <!-- Windows 10 compatibility -->
      <supportedOS Id="{8e0f7a12-bfb3-4fe8-b9a5-48fd50a15a9a}" />
    </application>
  </compatibility>
  ```

- 启用中的每监视器 DPI 感知*app.config*文件。

  Windows 窗体引入了一个新[ `<System.Windows.Forms.ApplicationConfigurationSection>` ](../configure-apps/file-schema/winforms/index.md)元素以支持新功能和自定义项添加从.NET Framework 4.7 开始。 若要充分利用支持高 DPI 的新功能，以下代码添加到应用程序配置文件。

  ```xml
  <System.Windows.Forms.ApplicationConfigurationSection>
    <add key="DpiAwareness" value="PerMonitorV2" />
  </System.Windows.Forms.ApplicationConfigurationSection>
  ```

  > [!IMPORTANT]
  > 在以前版本的.NET Framework，您可以使用清单添加高 DPI 支持。 不再建议使用此方法，因为它会替代 app.config 文件中定义的设置。

- 调用静态<xref:System.Windows.Forms.Application.EnableVisualStyles%2A>方法。

  这应该是应用程序的入口点中的第一个方法调用。 例如：

  ```csharp
  static void Main()
  {
      Application.EnableVisualStyles();
      Application.SetCompatibleTextRenderingDefault(false);
      Application.Run(new Form2());
  }
  ```

## <a name="opting-out-of-individual-high-dpi-features"></a>选择退出各个高 DPI 功能

设置`DpiAwareness`值设为`PerMonitorV2`使支持的.NET Framework 版本从.NET Framework 4.7 开始的所有高 DPI 感知功能。 通常情况下，这是适合大多数 Windows 窗体应用程序。 但是，你可能想要选择退出一个或多个单独的功能。 执行此操作的最重要的原因是，现有的应用程序代码已处理该功能。  例如，如果你的应用程序处理自动缩放，你可能想要禁用自动调整大小功能，如下所示：

```xml
<System.Windows.Forms.ApplicationConfigurationSection>
  <add key="DpiAwareness" value="PerMonitorV2" />
  <add key="EnableWindowsFormsHighDpiAutoResizing" value="false" />
</System.Windows.Forms.ApplicationConfigurationSection>
```

有关各个键及其值的列表，请参阅[Windows 窗体添加配置元素](../configure-apps/file-schema/winforms/windows-forms-add-configuration-element.md)。

## <a name="new-dpi-change-events"></a>新 DPI 更改事件

从.NET Framework 4.7 开始，三个新事件使您能够以编程方式处理动态 DPI 更改：

- <xref:System.Windows.Forms.Control.DpiChangedAfterParent>其父控件的 DPI 更改事件之后以编程方式更改控件的 DPI 设置或窗体已发生时激发。
- <xref:System.Windows.Forms.Control.DpiChangedBeforeParent>这在其父控件的 DPI 更改事件之前以编程方式更改控件的 DPI 设置或窗体已发生时被激发。
- <xref:System.Windows.Forms.Form.DpiChanged>这当前显示窗体的显示设备上的 DPI 设置更改时激发。

## <a name="new-helper-methods-and-properties"></a>新的帮助器方法和属性

.NET Framework 4.7 也将添加大量新的帮助器方法和属性，提供有关 DPI 缩放信息，可用于执行 DPI 缩放。 这些问题包括：

- <xref:System.Windows.Forms.Control.LogicalToDeviceUnits%2A>其中将一个值，从逻辑转换为设备像素为单位。

- <xref:System.Windows.Forms.Control.ScaleBitmapLogicalToDevice%2A>这可以扩展到设备的逻辑 DPI 的位图图像。

- <xref:System.Windows.Forms.Control.DeviceDpi%2A>它将返回当前设备的 DPI。

## <a name="versioning-considerations"></a>版本控制考虑事项

除了.NET Framework 4.7 和 Windows 10 创意者更新上运行，你的应用程序还可能会运行它不与高 DPI 改进兼容的环境中。 在这种情况下，你将需要开发的应用程序回退。 你可以执行[自定义绘图](./controls/user-drawn-controls.md)来处理缩放。

若要执行此操作，还需要确定您的应用程序正在其运行的操作系统。 可以使用如下所示的代码执行的操作：

```csharp
// Create a reference to the OS version of Windows 10 Creators Update.
Version OsMinVersion = new Version(10, 0, 15063, 0);

// Access the platform/version of the current OS.
Console.WriteLine(Environment.OSVersion.Platform.ToString());
Console.WriteLine(Environment.OSVersion.VersionString);

// Compare the current version to the minimum required version.
Console.WriteLine(Environment.OSVersion.Version.CompareTo(OsMinVersion));
```

请注意，是否未列出的应用程序清单中受支持的操作系统，你的应用程序不会成功检测 Windows 10。

此外可以检查生成应用程序时所针对的.NET framework 版本：

```csharp
Console.WriteLine(AppDomain.CurrentDomain.SetupInformation.TargetFrameworkName);
```

## <a name="see-also"></a>请参阅

- [Windows 窗体添加配置元素](../configure-apps/file-schema/winforms/windows-forms-add-configuration-element.md)
- [调整 Windows 窗体的大小和比例](adjusting-the-size-and-scale-of-windows-forms.md)
