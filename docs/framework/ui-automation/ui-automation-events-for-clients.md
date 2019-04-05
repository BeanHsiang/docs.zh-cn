---
title: 客户端的 UI 自动化事件
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, events for clients
- events, UI Automation clients
ms.assetid: b909e388-3f24-4997-b6d4-bd9c35c2dc27
ms.openlocfilehash: b384e3dde3f2f6ba75feef7954dc9872bd3e3cd5
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57676377"
---
# <a name="ui-automation-events-for-clients"></a>客户端的 UI 自动化事件
> [!NOTE]
>  本文档适用于想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空间中定义的托管 <xref:System.Windows.Automation> 类的 .NET Framework 开发人员。 有关最新信息[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]，请参阅[Windows 自动化 API:UI 自动化](https://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本主题介绍 UI 自动化客户端如何使用 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 事件。  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 允许客户端订阅关注的事件。 有了此功能，将不再需要频繁地轮询系统中的所有 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 元素来确定是否更改了任何信息、结构或状态，从而提高了性能。  
  
 由于能够只侦听定义范围内的事件，因此效率也得到了提高。 例如，客户端可以在树中的所有 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 元素上侦听焦点更改事件，也可以只在一个元素及其后代上侦听。  
  
> [!NOTE]
>  不要假定所有可能的事件都是由 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 提供程序引发的。 例如，并非所有属性更改都会导致 [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)] 和 [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] 控件的标准代理提供程序引发事件。  
  
 有关更广泛的视图[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]事件，请参阅[UI 自动化事件概述](../../../docs/framework/ui-automation/ui-automation-events-overview.md)。  
  
<a name="Subscribing_to_Events"></a>   
## <a name="subscribing-to-events"></a>订阅事件  
 客户端应用程序通过使用以下方法之一注册事件处理程序，从而订阅特定种类的事件。  
  
|方法|事件类型|事件参数类型|委托类型|  
|------------|----------------|--------------------------|-------------------|  
|<xref:System.Windows.Automation.Automation.AddAutomationFocusChangedEventHandler%2A>|焦点更改|<xref:System.Windows.Automation.AutomationFocusChangedEventArgs>|<xref:System.Windows.Automation.AutomationFocusChangedEventHandler>|  
|<xref:System.Windows.Automation.Automation.AddAutomationPropertyChangedEventHandler%2A>|属性更改|<xref:System.Windows.Automation.AutomationPropertyChangedEventArgs>|<xref:System.Windows.Automation.AutomationPropertyChangedEventHandler>|  
|<xref:System.Windows.Automation.Automation.AddStructureChangedEventHandler%2A>|结构更改|<xref:System.Windows.Automation.StructureChangedEventArgs>|<xref:System.Windows.Automation.StructureChangedEventHandler>|  
|<xref:System.Windows.Automation.Automation.AddAutomationEventHandler%2A>|所有其他事件（由 <xref:System.Windows.Automation.AutomationEvent> 标识）|<xref:System.Windows.Automation.AutomationEventArgs> 或 <xref:System.Windows.Automation.WindowClosedEventArgs>|<xref:System.Windows.Automation.AutomationEventHandler>|  
  
 在调用方法之前，必须创建一个委托方法来处理事件。 如果愿意，你可以在单一方法中处理不同种类的事件，并在多个调用中将此方法传递到表中的某个方法。 例如，可以将单一 <xref:System.Windows.Automation.AutomationEventHandler> 设置为根据 <xref:System.Windows.Automation.AutomationEventArgs.EventId%2A> 以不同的方式处理各种事件。  
  
> [!NOTE]
>  若要处理窗口关闭事件，请将传递到事件处理程序的参数类型转换为 <xref:System.Windows.Automation.WindowClosedEventArgs>。 由于窗口的 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 元素不再有效，因此无法使用 `sender` 参数来检索信息；请改用 <xref:System.Windows.Automation.WindowClosedEventArgs.GetRuntimeId%2A>。  
  
> [!CAUTION]
>  如果应用程序可能从自己的 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 中接收事件，请不要使用应用程序的 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 线程来订阅或取消订阅事件。 这样做可能会导致不可预知的行为。 有关更多信息，请参见 [UI Automation Threading Issues](../../../docs/framework/ui-automation/ui-automation-threading-issues.md)。  
  
 关闭时，或者当应用程序不再对 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 事件时，UI 自动化客户端应调用以下方法之一。  
  
|方法|描述|  
|------------|-----------------|  
|<xref:System.Windows.Automation.Automation.RemoveAutomationEventHandler%2A>|通过使用 <xref:System.Windows.Automation.Automation.AddAutomationEventHandler%2A> 取消注册已注册的事件处理程序。|  
|<xref:System.Windows.Automation.Automation.RemoveAutomationFocusChangedEventHandler%2A>|通过使用 <xref:System.Windows.Automation.Automation.AddAutomationFocusChangedEventHandler%2A> 取消注册已注册的事件处理程序。|  
|<xref:System.Windows.Automation.Automation.RemoveAutomationPropertyChangedEventHandler%2A>|通过使用 <xref:System.Windows.Automation.Automation.AddAutomationPropertyChangedEventHandler%2A> 取消注册已注册的事件处理程序。|  
|<xref:System.Windows.Automation.Automation.RemoveAllEventHandlers%2A>|取消注册所有已注册的事件处理程序。|  
  
 有关示例代码，请参阅[订阅 UI 自动化事件](../../../docs/framework/ui-automation/subscribe-to-ui-automation-events.md)。  
  
## <a name="see-also"></a>请参阅
- [订阅 UI 自动化事件](../../../docs/framework/ui-automation/subscribe-to-ui-automation-events.md)
- [UI 自动化事件概述](../../../docs/framework/ui-automation/ui-automation-events-overview.md)
- [UI 自动化属性概述](../../../docs/framework/ui-automation/ui-automation-properties-overview.md)
- [TrackFocus 示例](https://github.com/Microsoft/WPF-Samples/tree/master/Accessibility/FocusTracker)
