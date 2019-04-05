---
title: NotifyIcon 组件概述（Windows 窗体）
ms.date: 03/30/2017
f1_keywords:
- NotifyIcon
helpviewer_keywords:
- NotifyIcon component [Windows Forms], about NotifyIcon component
- system tray icons [Windows Forms], about system tray icons
- system tray icons [Windows Forms], using in Windows Forms
ms.assetid: 5b9189fa-d4ae-41a6-9b97-eb1f44bb1a69
ms.openlocfilehash: 430d869265b9add34c6de617a178aa27af6218f3
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57707620"
---
# <a name="notifyicon-component-overview-windows-forms"></a>NotifyIcon 组件概述（Windows 窗体）

Windows 窗体 <xref:System.Windows.Forms.NotifyIcon> 组件通常用于显示在后台运行且大部分时间不显示用户界面的进程的图标。 例如，可通过单击任务栏的状态通知区域中的图标访问的病毒防护程序。

## <a name="key-properties-of-notifyicons"></a>NotifyIcons 的键属性

每个 <xref:System.Windows.Forms.NotifyIcon> 组件均显示状态区域中的一个图标。 如果你有三个后台进程，并希望为每个进程显示一个图标，则必须添加三个 <xref:System.Windows.Forms.NotifyIcon> 组件到窗体。 <xref:System.Windows.Forms.NotifyIcon> 组件的键属性为 <xref:System.Windows.Forms.NotifyIcon.Icon%2A> 和 <xref:System.Windows.Forms.NotifyIcon.Visible%2A>。 <xref:System.Windows.Forms.NotifyIcon.Icon%2A> 属性设置状态区域中显示的图标。 为了显示图标，必须将 <xref:System.Windows.Forms.NotifyIcon.Visible%2A> 属性设置为 `true`。

## <a name="notifyicons-options"></a>NotifyIcons 选项

你可以将气球提示、快捷菜单和工具提示与 <xref:System.Windows.Forms.NotifyIcon> 进行关联，以辅助用户。

你可以通过调用 <xref:System.Windows.Forms.NotifyIcon.ShowBalloonTip%2A> 方法来指定需要气球提示显示的时间跨度，从而显示 <xref:System.Windows.Forms.NotifyIcon> 的气球提示。 还可以为气球提示的文本、图标和标题分别指定 <xref:System.Windows.Forms.NotifyIcon.BalloonTipText%2A>、<xref:System.Windows.Forms.NotifyIcon.BalloonTipIcon%2A> 和 <xref:System.Windows.Forms.NotifyIcon.BalloonTipTitle%2A>。 <xref:System.Windows.Forms.NotifyIcon> 组件还可以具有相关联的工具提示和快捷菜单。 有关详细信息，请参阅[ToolTip 组件概述](tooltip-component-overview-windows-forms.md)并[ContextMenu 组件概述](contextmenu-component-overview-windows-forms.md)。

## <a name="see-also"></a>请参阅

- <xref:System.Windows.Forms.NotifyIcon>
- [NotifyIcon 组件](notifyicon-component-windows-forms.md)