---
title: UI 自动化客户端的控件模式映射
ms.date: 03/30/2017
helpviewer_keywords:
- control patterns, for UI Automation clients
- UI Automation, clients, control patterns for
ms.assetid: 8b81645b-8be3-4e26-9c98-4fb0fceca06b
ms.openlocfilehash: b98735b111d634584ec019a75d942f39e38cc8c5
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57679575"
---
# <a name="control-pattern-mapping-for-ui-automation-clients"></a>UI 自动化客户端的控件模式映射
> [!NOTE]
>  本文档适用于想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空间中定义的托管 <xref:System.Windows.Automation> 类的 .NET Framework 开发人员。 有关最新信息[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]，请参阅[Windows 自动化 API:UI 自动化](https://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本主题列出了控件类型及其关联的控件模式。  
  
 下表将控件模式整理为以下类别：  
  
-   支持。 控件必须支持此控件模式。  
  
-   有条件支持。 控件可能支持此控件模式，具体取决于控件的状态。  
  
-   不支持。 控件不支持此控件模式；自定义控件可能支持此控件模式。  
  
> [!NOTE]
>  某些控件有条件支持一些控件模式，具体取决于控件的功能。 例如，菜单项控件有条件支持 <xref:System.Windows.Automation.InvokePattern>、 <xref:System.Windows.Automation.ExpandCollapsePattern>、 <xref:System.Windows.Automation.TogglePattern>或 <xref:System.Windows.Automation.SelectionItemPattern> 控件模式，具体取决于其菜单控件中的功能。  
  
<a name="control_mapping_clients"></a>   
## <a name="ui-automation-control-patterns-for-clients"></a>客户端的 UI 自动化控件模式  
  
|控件类型|支持|有条件支持|不支持|  
|------------------|---------------|-------------------------|-------------------|  
|Button|无|调用、切换、展开折叠|无|  
|Calendar|网格、表|选择、滚动|值|  
|复选框|切换|无|无|  
|组合框|展开/折叠|选择、值|Scroll|  
|数据网格|Grid|滚动、选择、表|无|  
|数据项|选择项|展开折叠、网格项、滚动项、表、切换、值|无|  
|Document|Text|滚动、值|无|  
|Edit|无|文本、范围值、值|无|  
|Group|无|展开/折叠|无|  
|Header|无|Transform|无|  
|标头项|无|转换、调用|无|  
|超链接|调用|值|无|  
|图像|无|网格项、表项|调用、选择项|  
|列表|无|网格、多个视图、滚动、选择|表|  
|列表项|选择项|展开折叠、网格项、调用、滚动项、切换、值|无|  
|菜单|无|无|无|  
|菜单栏|无|展开折叠、停靠、转换|无|  
|菜单项|无|展开折叠、调用、选择项、切换|无|  
|Pane|无|停靠。 滚动、转换|窗口|  
|进度栏|无|范围值、值|无|  
|单选按钮|选择项|无|切换|  
|滚动条|无|范围值|Scroll|  
|Separator|无|无|无|  
|Slider|无|范围值、选择、值|无|  
|Spinner|无|范围值、选择、值|无|  
|拆分按钮|调用、展开折叠|无|无|  
|状态栏|无|Grid|无|  
|Tab|选择|Scroll|无|  
|选项卡项|选择项|无|调用|  
|表|网格、网格项、表、表项|无|无|  
|Text|无|网格项、表项、文本|值|  
|Thumb|Transform|无|无|  
|标题栏|无|无|无|  
|工具栏|无|停靠、展开折叠、转换|无|  
|工具提示|无|文本、窗口|无|  
|树|无|滚动、选择|无|  
|树项|展开/折叠|调用，滚动项、选择项、切换|无|  
|窗口|转换、窗口|停靠|无|  
  
> [!NOTE]
>  如果控件类型没有可列出的受支持的控件模式，但具有一个或多个有条件支持的控件模式，则将始终支持这些有条件控件模式之一。  
  
## <a name="see-also"></a>请参阅
- [UI 自动化概述](../../../docs/framework/ui-automation/ui-automation-overview.md)
