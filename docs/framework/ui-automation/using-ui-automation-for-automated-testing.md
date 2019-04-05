---
title: 使用 UI 自动化进行自动化测试
ms.date: 03/30/2017
helpviewer_keywords:
- automated testing
- testing, UI Automation
- UI Automation, automated testing
ms.assetid: 3a0435c0-a791-4ad7-ba92-a4c1d1231fde
ms.openlocfilehash: e9bab754302252cdf4e4e9303ecc4a188e651ca9
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57678388"
---
# <a name="using-ui-automation-for-automated-testing"></a>使用 UI 自动化进行自动化测试
> [!NOTE]
>  本文档适用于想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空间中定义的托管 <xref:System.Windows.Automation> 类的 .NET Framework 开发人员。 有关最新信息[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]，请参阅[Windows 自动化 API:UI 自动化](https://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本概述介绍可如何将 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 用作一个用于在自动测试方案中进行编程访问的框架。  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 提供一个统一的对象模型，该模型使所有的 [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)] 框架均能够以可访问并易于实现自动化的方式公开复杂且丰富的功能。  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 是作为 [!INCLUDE[TLA#tla_aa](../../../includes/tlasharptla-aa-md.md)]的后续活动而开发的。 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)] 为现有框架，旨在提供使控件和应用程序可以访问的解决方案。 即使[!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)] 因辅助功能和自动化非常相似的要求发展成为该角色，但在设计时并未考虑测试自动化。 除了为辅助功能提供更完善的解决方案以外，[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]还专门用于提供进行自动测试的强大功能。 例如， [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)] 依赖于单个接口来公开 UI 相关信息和收集 AT 产品所需信息； [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 将这两个模型分开。  
  
 实现 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 需要提供程序和客户端，以便使其可以用作自动测试工具。 UI 自动化提供程序是 Microsoft Word、Excel 等应用程序以及其他第三方应用程序或基于 [!INCLUDE[TLA#tla_win](../../../includes/tlasharptla-win-md.md)] 操作系统的控件。 UI 自动化客户端包括自动测试脚本和辅助技术应用程序。  
  
> [!NOTE]
>  本概述的目的在于展示 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的新增及改进的自动测试功能。 本概述不提供有关辅助功能的信息，只有在必要时才会提到这些功能。  
  
<a name="Using_UI_Automation_During_Development"></a>   
## <a name="ui-automation-in-a-provider"></a>提供程序中的 UI 自动化  
 对于要自动化的 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] ，应用程序或控件的开发人员必须查看最终用户可以使用标准键盘和鼠标交互对 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 对象执行哪些操作。  
  
 确定这些键操作后，应在控件上实现相应的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 控件模式（即将 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 元素的功能和行为进行镜像的控件模式）。 例如，具有组合框控件（如运行对话框）的用户交互通常涉及展开和折叠组合框，以隐藏或显示项列表、从该列表中选择项或通过键盘输入添加新值。  
  
> [!NOTE]
>  对于其他辅助功能模型，开发人员必须直接从各个按钮、菜单或其他控件收集信息。 不便之处在于，每个控件类型都具有数十个次要变体。 也就是说，尽管某个按钮的十种变体全都以相同的方式工作且执行相同的功能，也必须将它们全部视为唯一控件。 无法知道这些控件在功能上是否相同。 所开发的控件模式可以表示这些常见的控件行为。 有关详细信息，请参阅 [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)。  
  
<a name="Implementing_UI_Automation"></a>   
### <a name="implementing-ui-automation"></a>实现 UI 自动化  
 如前所述，如果没有 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]提供的统一模型，则测试工具和开发人员必须了解特定于框架的信息才能公开该框架中控件的属性和行为。 因为可能有几个不同的 UI 框架在任一时间中的 Windows 操作系统，包括[!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)]， [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)]，Windows Presentation Foundation (WPF)，它可以是项艰巨的任务来测试多个应用程序看上去相似的控件。 例如，下表概述了检索与按钮控件相关联的名称（或文本）所需的框架特定属性名，并显示了单个等效的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 属性。  
  
|UI 自动化控件类型|UI 框架|特定于框架的属性|UI 自动化属性|  
|--------------------------------|------------------|---------------------------------|----------------------------|  
|Button|Windows Presentation Foundation|内容|NameProperty|  
|Button|Win32|标题|NameProperty|  
|图像|HTML|Alt|NameProperty|  
  
 UI 自动化提供程序负责将其控件的特定于框架的属性映射到等效的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 属性。  
  
 实现的信息[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]提供程序中，请参阅[UI 自动化提供程序的托管代码](../../../docs/framework/ui-automation/ui-automation-providers-for-managed-code.md)。 [UI Automation Control Patterns](../../../docs/framework/ui-automation/ui-automation-control-patterns.md) 和 [UI Automation Text Pattern](../../../docs/framework/ui-automation/ui-automation-text-pattern.md)中提供了有关实现控件模式的信息。  
  
<a name="Testing_with_UI_Automation"></a>   
## <a name="ui-automation-in-a-client"></a>客户端中的 UI 自动化  
 许多自动测试工具和方案的目标是以一致且可重复的方式操作用户界面。 该目标的范围包括：从对特定的控件进行单元测试，到录制并播放一些测试脚本，以便对一组控件循环执行一系列常规操作。  
  
 自动化应用程序存在的一个问题是难以将测试与动态目标同步。 这种动态目标的示例包括显示当前运行应用程序的列表的列表框控件（Windows 任务管理器中就包含这种列表框控件）。 由于该列表框中的项是不受测试应用程序的控制而动态更新的，因此总是无法在列表框中重复选择到前后一致的特定项。 尝试在不受测试应用程序控制的 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 中重复简单的焦点更改时，也会产生类似的问题。  
  
<a name="Programmatic_Access"></a>   
### <a name="programmatic-access"></a>编程访问  
 使用编程访问可以通过代码模仿由传统鼠标和键盘输入展开的任何交互和体验。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 通过五个组件实现编程访问：  
  
-   借助 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 树，可以方便地在 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]结构中导航。 树是基于 hWnd 的集合生成的。 有关详细信息，请参阅 [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)。  
  
-   自动化元素是 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]中的独立组件。 这些组件的粒度级通常比 hWnd 更精细。 有关详细信息，请参阅 [UI Automation Control Types Overview](../../../docs/framework/ui-automation/ui-automation-control-types-overview.md)。  
  
-   自动化属性提供有关 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 元素的特定信息。 有关更多信息，请参见 [UI Automation Properties Overview](../../../docs/framework/ui-automation/ui-automation-properties-overview.md)。  
  
-   控件模式定义了控件功能的特定方面；控件模式可以由属性、方法、事件和结构信息组成。 有关详细信息，请参阅 [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)。  
  
-   自动化事件提供事件通知和信息。 有关更多信息，请参见 [UI Automation Events Overview](../../../docs/framework/ui-automation/ui-automation-events-overview.md)。  
  
<a name="Key_properties_critical_to_test_automation"></a>   
### <a name="key-properties-for-test-automation"></a>测试自动化的关键属性  
 由于可以对 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 中的任何控件进行唯一标识，并且以后还能查找该控件，因此，自动测试应用程序可在此基础上对该 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]执行相应的操作。 客户端和提供程序使用一些 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 属性来帮助实现此功能。  
  
#### <a name="automationid"></a>AutomationID  
 将自动化元素从其同级中单独标识出来。 <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty> 不同于 <xref:System.Windows.Automation.AutomationElement.NameProperty> 等属性，前者并未经过本地化；而对于后者，如果产品需要以多种语言提供，则这些属性通常已本地化。 请参阅 [Use the AutomationID Property](../../../docs/framework/ui-automation/use-the-automationid-property.md)。  
  
> [!NOTE]
>  <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty> 不保证整个自动化树使用唯一标识。 例如，一个应用程序可能包含具有多个顶级菜单项的菜单控件，而这些顶级菜单项又具有多个子菜单项。 可以通过常规架构（如“Item1、Item2、Item3 等”）标识这些二级菜单项，并允许顶级菜单项中的子菜单项使用重复的标识符。  
  
#### <a name="controltype"></a>ControlType  
 标识由自动化元素表示的控件类型。 通过了解控件类型可以推断出重要的信息。 请参阅 [UI Automation Control Types Overview](../../../docs/framework/ui-automation/ui-automation-control-types-overview.md)。  
  
#### <a name="nameproperty"></a>NameProperty  
 这是标识或说明控件的文本字符串。 应谨慎使用<xref:System.Windows.Automation.AutomationElement.NameProperty> ，因为可对其进行本地化。 请参阅 [UI Automation Properties Overview](../../../docs/framework/ui-automation/ui-automation-properties-overview.md)。  
  
<a name="Steps_Required_To_Automate_the_UI_in_a_Test_Application"></a>   
### <a name="implementing-ui-automation-in-a-test-application"></a>在测试应用程序中实现 UI 自动化  
  
|||  
|-|-|  
|添加 UI 自动化引用。|下面列出了 UI 自动化客户端所必需的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] dll。<br /><br /> -Uiautomationclient.dll 访问[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]客户端 Api。<br />-Uiautomationclientsideprovider.dll 可以自动执行[!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)]控件。 请参阅 [UI Automation Support for Standard Controls](../../../docs/framework/ui-automation/ui-automation-support-for-standard-controls.md)。<br />-UIAutomationTypes.dll 提供对中定义的特定类型的访问[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]。|  
|添加 <xref:System.Windows.Automation> 命名空间。|此命名空间包含 UI 自动化客户端使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 的功能（文本处理除外）所需的一切内容。|  
|添加 <xref:System.Windows.Automation.Text> 命名空间。|此命名空间包含 UI 自动化客户端使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 文本处理的功能所需的一切内容。|  
|查找相关控件|自动测试脚本可以查找表示自动化树中相关控件的 UI 自动化元素。<br /><br /> 可使用多种方法来通过代码获取 UI 自动化元素。<br /><br /> -查询[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]使用<xref:System.Windows.Automation.Condition>语句。 这通常是使用中性语言 <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty> 的位置。 **注意：**<xref:System.Windows.Automation.AutomationElement.AutomationIdProperty>可以使用能够详细列举的 Inspect.exe 之类的工具获取[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]控件的属性。 <br /><br /> -使用<xref:System.Windows.Automation.TreeWalker>类，以遍历整个[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]树或其子集。<br />-跟踪焦点。<br />-使用该控件的 hWnd。<br />-使用屏幕位置，例如鼠标光标的位置。<br /><br /> 请参见 [Obtaining UI Automation Elements](../../../docs/framework/ui-automation/obtaining-ui-automation-elements.md)|  
|获取控件模式|控件模式公开在功能上相似的控件的常见行为。<br /><br /> 找到需要测试的控件之后，自动测试脚本从这些 UI 自动化元素获取相关的控件模式。 例如，用于典型按钮功能的 <xref:System.Windows.Automation.InvokePattern> 控件模式或用于窗口功能的 <xref:System.Windows.Automation.WindowPattern> 控件模式。<br /><br /> 请参阅 [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)。|  
|自动化 UI|自动测试脚本现在可以使用 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 控件模式公开的信息和功能来控制 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 框架中的任何相关 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 。|  
  
<a name="Supporting_tools"></a>   
## <a name="related-tools-and-technologies"></a>相关的工具和技术  
 有许多支持使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]进行自动测试的相关工具和技术。  
  
-   是 Inspect.exe[!INCLUDE[TLA#tla_gui](../../../includes/tlasharptla-gui-md.md)]应用程序，可用于收集[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]提供程序和客户端开发和调试信息。 中包含 Inspect.exe [!INCLUDE[TLA#tla_winfxsdk](../../../includes/tlasharptla-winfxsdk-md.md)]。  
  
-   MSAABridge 向 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 客户端公开 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)] 信息。 将 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 桥接到 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)] 的主要目的是使现有的 [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)] 客户端具有与已实现 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的任何框架进行交互的能力。  
  
<a name="Security"></a>   
## <a name="security"></a>安全性  
 有关安全信息，请参阅 [UI Automation Security Overview](../../../docs/framework/ui-automation/ui-automation-security-overview.md)。  
  
## <a name="see-also"></a>请参阅
- [UI 自动化基础知识](../../../docs/framework/ui-automation/index.md)
