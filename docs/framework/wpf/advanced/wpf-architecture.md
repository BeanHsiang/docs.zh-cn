---
title: WPF 体系结构
ms.date: 03/30/2017
helpviewer_keywords:
- properties [WPF], attached
- attached properties [WPF]
- architecture [WPF]
- unmanaged components [WPF]
- affinity thread [WPF]
- Storyboards [WPF]
- milcore [WPF]
- components [WPF], unmanaged
- painter's algorithm
- interfaces [WPF], INotifyPropertyChange
- CommandBindings [WPF]
- data templates [WPF]
- thread [WPF], affinity
ms.assetid: 8579c10b-76ab-4c52-9691-195ce02333c8
ms.openlocfilehash: dee88ceb82528955d8809214bff474b92233d28c
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57362002"
---
# <a name="wpf-architecture"></a>WPF 体系结构
本主题提供 Windows Presentation Foundation (WPF) 类层次结构的指导的教程。 本主题涵盖了 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的大部分主要子系统，并说明它们的交互方式。 本主题还详细介绍了 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 架构师所做的一些选择。  
  
  
<a name="System_Object"></a>   
## <a name="systemobject"></a>System.Object  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 主要编程模型通过托管代码公开。 在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的早期设计阶段，曾有过大量关于如何界定系统的托管组件和非托管组件的争论。 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 提供一系列的功能，可以提高开发效率和可靠性（包括内存管理、错误处理和通用类型系统等），但这是需要付出代价的。  
  
 下图说明了 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的主要组件。 关系图的红色部分（PresentationFramework、PresentationCore 和 milcore）是 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的主要代码部分。 在这些组件中，只有一个是非托管组件 - milcore。 milcore 是以非托管代码编写的，目的是实现与 [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)] 的紧密集成。 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中的所有显示均通过 [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)] 引擎完成，因此硬件和软件呈现都很高效。 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 还要求对内存和执行进行精细控制。 milcore 中的组合引擎受性能影响极大，需要放弃 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 的许多优点来提高性能。  
  
 ![WPF 在 .NET Framework 中的位置。](./media/wpf-architect1.PNG "wpf_architect1")  
  
 本主题的后面部分将讨论 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的托管和非托管部分之间的通信。 下面介绍托管编程模型的其余部分。  
  
<a name="System_Threading_DispatcherObject"></a>   
## <a name="systemthreadingdispatcherobject"></a>System.Threading.DispatcherObject  
 中的大多数对象[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]派生自<xref:System.Windows.Threading.DispatcherObject>，后者提供的基本构造来处理并发和线程处理。 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 基于调度程序实现的消息系统。 其工作方式与常见的 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] 消息泵非常类似；事实上，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 调度程序使用 User32 消息执行跨线程调用。  
  
 要讨论 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中的并发，首先必须真正理解两个核心概念 - 调度程序和线程关联。  
  
 在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的设计阶段，目标是移动到单一线程的执行，但这不是一种与线程“关联的”模型。 当一个组件使用执行线程的标识来存储某种类型的状态时，将发生线程关联。 最常见的形式是使用线程本地存储 (TLS) 来存储状态。 线程关联要求执行的每个逻辑线程仅由操作系统中的一个物理线程所拥有，这将占用大量内存。 最后，WPF 的线程处理模型通过线程关联与单一线程执行的现有 User32 线程处理模型保持同步。 主要原因是互操作性 - 类似于 [!INCLUDE[TLA2#tla_ole2.0](../../../../includes/tla2sharptla-ole2-0-md.md)] 的系统、剪贴板和 Internet Explorer 均需要单一线程关联 (STA) 执行。  
  
 假设你具有带有 STA 线程的对象，则需要在线程之间通信并验证你是否位于正确的线程上的一种方法。 调度程序的作用就在于此。 调度程序是一个基本的消息调度系统，具有多个按优先顺序排列的队列。 消息的示例包括原始输入通知（鼠标移动）、框架函数（布局）或用户命令（执行此方法）。 通过派生自<xref:System.Windows.Threading.DispatcherObject>，创建[!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)]对象具有 STA 行为的并将获得一个指向调度程序在创建时。  
  
<a name="System_Windows_DependencyObject"></a>   
## <a name="systemwindowsdependencyobject"></a>System.Windows.DependencyObject  
 生成 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 时使用的主要体系结构原理之一是首选属性而不是方法或事件。 属性具有声明性，可更方便地指定用途而不是操作。 它还支持模型驱动或数据驱动的系统，以显示用户界面内容。 这种理念的预期效果是创建更多可以绑定到的属性，从而更好地控制应用程序的行为。  
  
 为了更加充分地利用由属性驱动的系统，需要一个比 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 提供的功能更丰富的属性系统。 这种丰富性的一个简单示例是更改通知。 若要实现双向绑定，需要绑定的双方支持更改通知。 若要使行为与属性值相关联，需要在属性值更改时收到通知。 Microsoft.NET Framework 中的一个接口， **INotifyPropertyChange**，这允许对象发布更改通知，但它是可选的。  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 提供了更丰富的属性系统，派生自<xref:System.Windows.DependencyObject>类型。 该属性系统实际是一个“依赖”属性系统，因为它会跟踪属性表达式之间的依赖关系，并在依赖关系更改时自动重新验证属性值。 例如，如果您有一个继承的属性 (如<xref:System.Windows.Controls.Control.FontSize%2A>)，如果继承值的元素的父级发生属性更改，系统会自动更新。  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 属性系统的基础是属性表达式的概念。 在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的第一个版本中，属性表达式系统是关闭的，表达式均作为框架的一部分提供。 表达式致使属性系统不具有数据绑定、样式调整或继承硬编码，而是由框架内后面的层来提供这些功能。  
  
 属性系统还提供属性值的稀疏存储。 因为对象可能有数十个（如果达不到上百个）属性，并且大部分值处于其默认状态（被继承、由样式设置等），所以并非对象的每个实例都需要具有在其上定义的每个属性的完全权重。  
  
 属性系统的最后一个新功能是附加属性的概念。 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 元素是基于组合和组件重用的原则生成的。 它通常是这种情况，某些包含元素 (如<xref:System.Windows.Controls.Grid>布局元素) 需要在子元素来控制其行为 （如行/列信息中） 上的其他数据。 任何对象都可以为任何其他对象提供属性定义，而不是将所有这些属性与每个元素相关联。 这与 JavaScript 中的“expando”功能相似。  
  
<a name="System_Windows_Media_Visual"></a>   
## <a name="systemwindowsmediavisual"></a>System.Windows.Media.Visual  
 定义一个系统后，下一步是将像素绘制到屏幕上。 <xref:System.Windows.Media.Visual>类提供了用于每个可以选择性地包含绘制指令以及有关如何呈现这些指令 （剪裁、 转换等） 的元数据生成视觉对象的树。 <xref:System.Windows.Media.Visual> 设计为极其轻量且灵活，因此大部分功能均未公开[!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)]公开并且非常依赖受保护的回调函数。  
  
 <xref:System.Windows.Media.Visual> 是真正的入口点[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]复合系统。 <xref:System.Windows.Media.Visual> 是托管这两个子系统之间的连接点[!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)]和非托管的 milcore。  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 通过遍历由 milcore 管理的非托管数据结构来显示数据。 这些结构（称为组合节点）代表层次结构显示树，其中每个节点都有呈现指令。 只能通过消息传递协议来访问此树（如下图右侧所示）。  
  
 编程时[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]，创建<xref:System.Windows.Media.Visual>元素和派生的类型，它们在内部与此消息传递协议通过此组合树进行通信。 每个<xref:System.Windows.Media.Visual>在[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]可能会创建一个、 none、 或多个组合节点。  
  
 ![Windows Presentation Foundation 可视化树。](./media/wpf-architecture2.PNG "wpf_architecture2")  
  
 请注意一个非常重要的体系结构细节 - 会缓存整个可视化树和绘制指令。 在图形方面，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 使用一个保留的绘制系统。 这可以实现以高刷新率重绘系统，并且组合系统不会阻止对用户代码的回调。 这有助于防止出现应用程序无响应的情况。  
  
 关系图中容易忽略的另一个重要细节是系统实际执行组合的方式。  
  
 在 User32 和 [!INCLUDE[TLA2#tla_gdi](../../../../includes/tla2sharptla-gdi-md.md)] 中，系统在一个即时模式剪裁系统上工作。 当需要绘制一个组件时，系统会建立一个剪裁边界，在此边界外，不允许组件接触像素，然后会要求组件在该框中绘制像素。 此系统在内存受限的系统上工作良好，因为当某些内容更改时，只需处理受影响的组件即可 - 不会由两个组件同时处理一个像素的颜色。  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 使用“绘画器的算法”绘制模型。 要求每个组件从显示内容的背面绘制到正面，而不是剪裁每个组件。 这允许每个组件在先前组件的显示内容上绘制。 此模型的优点是可以生成部分透明的复杂形状。 通过使用当今的新式图形硬件，此模型的速度相对较快（创建 User32/ [!INCLUDE[TLA2#tla_gdi](../../../../includes/tla2sharptla-gdi-md.md)] 时则不然）。  
  
 如上所述，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的一个核心原理是转移到一个更具声明性且“以属性为中心”的编程模型。 在可视化系统中，这体现在有意思的几个方面。  
  
 首先，对于保留的模式图形系统，这实际上是从命令性 DrawLine/DrawLine 类型模型移动到面向数据的模型 new Line()/new Line()。 通过这种向数据驱动的绘制的移动，可以使用属性表达绘制指令上的复杂操作。 从派生类型<xref:System.Windows.Media.Drawing>实际上是呈现的对象模型。  
  
 第二，如果评估动画系统，你会发现它几乎是完全声明性的。 可以将动画表示为动画对象上的一组属性，无需要求开发人员计算下一个位置或下一个颜色。 这些动画可以表达开发人员或设计人员的意图（在 5 秒内将此按钮从一个位置移动到另一个位置），系统可以确定完成此任务的最高效方式。  
  
<a name="System_Windows_UIElement"></a>   
## <a name="systemwindowsuielement"></a>System.Windows.UIElement  
 <xref:System.Windows.UIElement> 定义核心子系统，包括布局、 输入和事件。  
  
 布局是 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中的核心概念。 在许多系统中，可能有一组固定的布局模型（HTML 支持三种布局模型：流、绝对和表），也可能没有布局模型（User32 实际仅支持绝对定位）。 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 先假设开发人员和设计人员需要灵活的可扩展布局模型，该模型可能是由属性值而不是命令性逻辑驱动的。 在<xref:System.Windows.UIElement>级别，引入布局的基本协定-阶段使用的模型的两阶段<xref:System.Windows.UIElement.Measure%2A>和<xref:System.Windows.UIElement.Arrange%2A>传递。  
  
 <xref:System.Windows.UIElement.Measure%2A> 允许组件确定所要采取的大小。 这是从单独阶段<xref:System.Windows.UIElement.Arrange%2A>因为有很多情况下，父元素会要求子测量若干次以确定其最佳位置和大小。 父元素要求子元素测量这一事实体现了 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的另一关键原则 - 调整内容大小。 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中的所有控件支持调整到内容自然大小的功能。 这使本地化更加容易，并可实现调整内容大小时进行动态元素布局。 <xref:System.Windows.UIElement.Arrange%2A>阶段允许父元素定位并确定每个子级的最终大小。  
  
 很多时间通常会花费谈论的输出一端[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]–<xref:System.Windows.Media.Visual>和相关对象。 然而，在输入端也有许多创新。 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 输入模型中的最基本更改也许是一致模型，借助此模型可通过系统对输入事件进行路由。  
  
 输入是作为内核模式设备驱动程序上的信号发出的，并通过涉及 Windows 内核和 User32 的复杂过程路由到正确的进程和线程。 与输入相对应的 User32 消息路由到 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 后，转换为 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 原始输入消息，并发送到调度程序。 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 允许将原始输入事件转换为多个实际事件，在保证传递到位的情况下在低系统级别实现类似“MouseEnter”的功能。  
  
 每个输入事件至少会转换为两个事件 -“预览”事件和实际事件。 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中的所有事件都具有通过元素树路由的概念。 事件被称为"浮升"如果用户从目标树中向上遍历到根目录，并从根开始并遍历到目标被称为"隧道"。 输入预览事件隧道，使树中的任何元素都有机会筛选事件或对事件采取操作。 然后，常规（非预览）事件将从目标向上浮升到根。  
  
 隧道和浮升阶段之间的划分使键盘快捷键等功能的实现在复合环境中采用一致的方式。 在 User32 中，可以通过使用一个全局表来实现键盘快捷键，该表中包含你希望支持的所有快捷键（Ctrl+N 映射到“新建”）。 在应用程序的调度程序中，可以调用 **TranslateAccelerator**，它会探查 User32 中的输入消息，并确定是否有任何消息与已注册的快捷键匹配。 在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中，上述内容无效，因为系统是完全“可组合”的 - 任何元素都可以处理和使用任何键盘快捷键。 将此两阶段模型用于输入，可允许组件实现其自己的“TranslateAccelerator”。  
  
 若要进一步此步骤，<xref:System.Windows.UIElement>还引入了 CommandBindings 的概念。 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]命令系统允许开发人员的方式定义功能命令终结点 – 内容实现<xref:System.Windows.Input.ICommand>。 命令绑定使元素可以定义输入笔势 (Ctrl+N) 和命令（“新建”）之间的映射。 输入笔势和命令定义都是可扩展的，并且可以在使用时联系到一起。 这使得一些操作（例如，允许最终用户自定义其要在应用程序内使用的键绑定）显得无关紧要。  
  
 至此，本主题已重点讨论了 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的“核心”功能 - PresentationCore 程序集中实现的功能。 生成时[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]、 明确划分基础部分 (如与布局的协定**度量值**并**排列**) 和框架部分 （例如特定的实现像布局<xref:System.Windows.Controls.Grid>) 是所需的结果。 目标是提供在堆栈中处于较低位置的可扩展性点，这将允许外部开发人员在需要时创建自己的框架。  
  
<a name="System_Windows_FrameworkElement"></a>   
## <a name="systemwindowsframeworkelement"></a>System.Windows.FrameworkElement  
 <xref:System.Windows.FrameworkElement> 可以查看两个不同的方式。 它在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的较低层中引入的子系统上引入一组策略和自定义项。 它还引入了一组新的子系统。  
  
 通过引入的主要策略<xref:System.Windows.FrameworkElement>与应用程序布局。 <xref:System.Windows.FrameworkElement> 基础上引入的基本布局协定构建<xref:System.Windows.UIElement>并添加布局"插槽"可使布局作者具有一组一致的属性驱动的布局语义更方便的概念。 属性，如<xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>， <xref:System.Windows.FrameworkElement.VerticalAlignment%2A>， <xref:System.Windows.FrameworkElement.MinWidth%2A>，和<xref:System.Windows.FrameworkElement.Margin%2A>（若要仅举几例） 派生自的所有组件<xref:System.Windows.FrameworkElement>在布局容器内一致的行为。  
  
 <xref:System.Windows.FrameworkElement> 此外可以更方便地[!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)]的核心层中找到的许多功能认识[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]。 例如，<xref:System.Windows.FrameworkElement>提供直接访问权限通过动画<xref:System.Windows.FrameworkElement.BeginStoryboard%2A>方法。 一个<xref:System.Windows.Media.Animation.Storyboard>地针对一组属性的多个动画编写脚本。  
  
 最重要的两点，<xref:System.Windows.FrameworkElement>引入了将数据绑定和样式。  
  
 曾经使用 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 或 [!INCLUDE[TLA#tla_aspnet](../../../../includes/tlasharptla-aspnet-md.md)] 创建应用程序 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 的用户应当对 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中的数据绑定子系统较为熟悉。 在上述每个系统中，可通过一种简单的方式来表达希望将给定元素中的一个或多个属性绑定到一个数据片段。 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 完全支持属性绑定、转换和列表绑定。  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中数据绑定的最值得关注的功能之一是引入了数据模板。 利用数据模板，可以通过声明方式指定某个数据片断的可视化方式。 无需创建可绑定到数据的自定义用户界面，而是转而让数据来确定要创建的显示内容。  
  
 样式实际上是轻量型的数据绑定。 使用样式，可以将共享定义的一组属性绑定到元素的一个或多个实例。 样式应用到元素通过显式引用 (通过设置<xref:System.Windows.FrameworkElement.Style%2A>属性) 或通过关联与样式来隐式[!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)]元素的类型。  
  
<a name="System_Windows_Controls_Control"></a>   
## <a name="systemwindowscontrolscontrol"></a>System.Windows.Controls.Control  
 控件的最重要功能是模板化。 如果将 WPF 的组合系统视为一个保留模式绘制系统，则控件可通过模板化以一种参数化的声明性方式描述其绘制。 一个<xref:System.Windows.Controls.ControlTemplate>实际上只不过是一个脚本来创建一组子元素，同时绑定到由控件提供的属性。  
  
 <xref:System.Windows.Controls.Control> 提供了一组常用属性<xref:System.Windows.Controls.Control.Foreground%2A>， <xref:System.Windows.Controls.Control.Background%2A>， <xref:System.Windows.Controls.Control.Padding%2A>，仅举几例，模板作者可以使用自定义控件的显示。 控件的实现提供了数据模型和交互模型。 交互模型定义了一组命令（如窗口的“关闭”），以及到输入笔势的绑定（如单击窗口右上角的红叉）。 数据模型提供了一组属性，用于自定义交互模型或自定义显示内容（由模板确定）。  
  
 数据模型（属性）、交互模型（命令和事件）及显示模型（模板）之间的划分，可实现对控件的外观和行为的完全自定义。  
  
 最常见的控件数据模型是内容模型。 如果您看一下控件喜欢<xref:System.Windows.Controls.Button>，你将看到它有一个名为"Content"的类型属性<xref:System.Object>。 在 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 和 [!INCLUDE[TLA#tla_aspnet](../../../../includes/tlasharptla-aspnet-md.md)] 中，此属性通常是一个字符串 - 不过，这会限制可以在按钮中添加的内容类型。 按钮的内容可以是简单的字符串、复杂的数据对象或整个元素树。 如果是数据对象，可以使用数据模板构造显示内容。  
  
<a name="Summary"></a>   
## <a name="summary"></a>总结  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 可创建动态的数据驱动的演示系统。 系统的每一部分均可通过驱动行为的属性集来创建对象。 数据绑定是系统的基础部分，在每一层中均进行了集成。  
  
 传统的应用程序创建一个显示内容，然后绑定到某些数据。 在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中，控件的所有内容、显示内容的所有方面都是由某种类型的数据绑定生成的。 通过在按钮内部创建复合控件并将其显示内容绑定到按钮的内容属性，会显示按钮中的文本。  
  
 当开始开发基于 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的应用程序时，你应感到非常熟悉。 设置属性、使用对象和数据绑定的方式与使用 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 或 [!INCLUDE[TLA#tla_aspnet](../../../../includes/tlasharptla-aspnet-md.md)] 的方式极为相似。 如果对 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 体系结构有更深的了解，将能够创建更丰富的应用程序，这些应用程序在根本上会将数据视为应用程序的核心驱动要素。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Media.Visual>
- <xref:System.Windows.UIElement>
- <xref:System.Windows.Input.ICommand>
- <xref:System.Windows.FrameworkElement>
- <xref:System.Windows.Threading.DispatcherObject>
- <xref:System.Windows.Input.CommandBinding>
- <xref:System.Windows.Controls.Control>
- [数据绑定概述](../data/data-binding-overview.md)
- [布局](layout.md)
- [动画概述](../graphics-multimedia/animation-overview.md)
