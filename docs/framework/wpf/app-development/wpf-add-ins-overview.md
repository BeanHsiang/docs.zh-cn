---
title: WPF 外接程序概述
ms.date: 03/30/2017
helpviewer_keywords:
- add-ins and XAML browser applications [WPF]
- add-ins overview [WPF]
- add-ins [WPF], performance
- add-ins [WPF], benefits
- .NET Framework add-in model [WPF]
- add-ins [WPF], user interface
- add-ins and the user interface [WPF]
- add-ins [WPF], architecture
- add-ins [WPF], limitations
ms.assetid: 00b4c776-29a8-4dba-b603-280a0cdc2ade
ms.openlocfilehash: 859e586d6cb0b334a7ad766de5d3aabb0e1864ac
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57365836"
---
# <a name="wpf-add-ins-overview"></a>WPF 外接程序概述
<a name="Introduction"></a> .NET Framework 包括开发人员可用于创建支持外接程序扩展性的应用程序的外接程序模型。 借助此外接程序模型，可以创建与应用程序功能集成并进行扩展的外接程序。 在某些情况下，应用程序还需要显示外接程序提供的用户界面。本主题介绍 WPF 增加.NET Framework 外接程序模型若要启用这些方案，它、 其优点和局限性的体系结构的内容。  
  

  
<a name="Requirements"></a>   
## <a name="prerequisites"></a>系统必备  
 熟悉.NET Framework 外接程序模型是必需的。 有关详细信息，请参阅[外接程序和扩展性](/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100))。  
  
<a name="AddInsOverview"></a>   
## <a name="add-ins-overview"></a>外接程序概述  
 为了需要对应用程序重新编译和重新部署才能引入新功能这一复杂过程，应用程序实现了扩展机制，使开发者（包括第一方和第三方）能够创建与应用程序集成的其他应用程序。 支持此扩展性类型的最常见方式是，使用外接程序（也称为“加载项”和“插件”）。 通过外接程序公开扩展性的实际应用程序示例包括：  
  
-   Internet Explorer 加载项。  
  
-   Windows Media Player 插件。  
  
-   Visual Studio 外接程序。  
  
 例如，通过 Windows Media Player 外接程序模型，第三方开发人员可以实现“插件”，从而以各种方式对 Windows Media Player 进行扩展，包括为 Windows Media Player 本身不支持的媒体格式（例如 DVD、MP3）创建解码器和编码器，创建音频效果和外观。 尽管有一些实体和行为是所有外接程序模型共有的，但会生成每个外接程序模型以公开某个应用程序的特有功能。  
  
 典型外接程序扩展性解决方案的三大实体是“协定”、“外接程序”和“主机应用程序”。 协定会定义外接程序与主机应用程序之间的两种集成方式：  
  
-   外接程序集成主机应用程序所实现的功能。  
  
-   主机应用程序公开供外接程序集成的功能。  
  
 为了使外接程序能发挥作用，主机应用程序需要在运行时找到它们并进行加载。 因此，支持外接程序的应用程序需要承担以下附加的职责：  
  
-   **发现**:查找遵循主机应用程序支持的协定的外接程序。  
  
-   **激活**:正在加载、 运行和建立与外接程序的通信。  
  
-   **隔离**:使用应用程序域或进程建立隔离边界，保护应用程序免受潜在的安全和外接程序执行问题。  
  
-   **通信**:允许加载项和主机应用程序彼此通信跨隔离边界，通过调用方法并传递数据。  
  
-   **生存期管理**:加载和卸载应用程序域和进程以干净、 可预测的方式 (请参阅[应用程序域](../../app-domains/application-domains.md))。  
  
-   **版本控制**:确保，主机应用程序和外接程序仍可进行通信时创建的新版本。  
  
 总之，开发一个可靠的外接程序模型不是一项简单的任务。 出于此原因，.NET Framework 构建外接程序模型提供一种基础结构。  
  
> [!NOTE]
>  有关外接程序的更多详细信息，请参阅[外接程序和扩展性](/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100))。  
  
<a name="NETFrameworkAddInModelOverview"></a>   
## <a name="net-framework-add-in-model-overview"></a>.NET Framework 外接程序模型概述  
 在中找到.NET Framework 外接程序模型，<xref:System.AddIn>命名空间包含一组旨在简化开发外接程序扩展性的类型。 .NET Framework 外接程序模型的基本单元是*协定*、 用于定义如何主机应用程序和外接程序与彼此通信。 会使用特定于主机应用程序的协定*视图*向主机应用程序公开协定。 同样，向外接程序公开特定于外接程序的协定*视图*。 使用*适配器*，主机应用程序和外接程序可以在它们各自的协定视图之间进行通信。 协定、视图和适配器称为管道段，一组相关的管道段组成一条*管道*。 管道是在其.NET Framework 外接程序模型支持发现、 激活、 安全隔离、 执行隔离 （使用应用程序域和进程）、 通信、 生存期管理和版本控制的基础。  
  
 所有这些支持使得开发人员能够生成与主机应用程序的功能相集成的外接程序。 但是，某些情况下需要主机应用程序显示用户界面提供的外接程序。由于.NET Framework 中的每个演示文稿技术都有其自己的模型用于实现用户界面，.NET Framework 外接程序模型不支持任何特定的显示技术。 相反，WPF 扩展模型外, 接程序的 UI 支持.NET Framework 外接程序。  
  
<a name="WPFAddInModel"></a>   
## <a name="wpf-add-ins"></a>WPF 外接程序  
 WPF 中，与.NET Framework 外接程序模型，结合使用，可处理各种要求主机应用程序显示外接程序从用户界面的方案。具体而言，处理这些情况由 WPF 使用以下两种编程模型：  
  
1.  **外接程序返回 UI**。 外接程序返回 UI 到主机应用程序通过方法调用，如协定所定义的。 此方案可用于以下情况：  
  
    -   返回的外接程序的 UI 的外观取决于数据或条件可仅在运行时，例如动态生成的报告。  
  
    -   为服务提供的外接程序的 UI 与从外接程序可以使用的主机应用程序的 UI。  
  
    -   外接程序主要执行某项服务的主机应用程序，并向主机应用程序的 ui 报告状态。  
  
2.  **外接程序为 UI**。 外接程序是一个 UI，如协定所定义的。 此方案可用于以下情况：  
  
    -   外接程序提供的服务都需要显示，例如广告。  
  
    -   服务提供的外接程序的 UI 是普遍适用于所有主机应用程序可以使用该外接程序，如计算器或颜色选取器。  
  
 这些方案需要，可以主机应用程序和外接程序应用程序域之间传递 UI 对象。 自.NET Framework 外接程序模型依赖于远程处理应用程序域之间进行通信，它们之间传递的对象必须可远程处理。  
  
 可远程处理的对象是某个类的实例，并执行以下一个或多个任务：  
  
-   派生自<xref:System.MarshalByRefObject>类。  
  
-   实现 <xref:System.Runtime.Serialization.ISerializable> 接口。  
  
-   具有<xref:System.SerializableAttribute>应用属性。  
  
> [!NOTE]
>  有关创建可远程处理.NET Framework 对象的详细信息，请参阅[使对象可远程处理](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/wcf3swha(v=vs.100))。  
  
 WPF UI 类型不可远程处理。 若要解决此问题，WPF 扩展了.NET Framework 外接程序模型以启用 WPF UI 的外接程序创建要显示从主机应用程序。 通过两种类型的 wpf 提供此支持：<xref:System.AddIn.Contract.INativeHandleContract>接口和实现的两个静态方法<xref:System.AddIn.Pipeline.FrameworkElementAdapters>类：<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A>和<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>。 从较高层面来看，这些类型和方法按以下方式使用：  
  
1.  WPF 要求由外接程序提供的用户界面是直接或间接派生的类<xref:System.Windows.FrameworkElement>，如形状、 控件、 用户控件、 布局面板和页面。  
  
2.  无论协定声明，将外接程序与主机应用程序之间传递 UI，它必须声明为<xref:System.AddIn.Contract.INativeHandleContract>(不<xref:System.Windows.FrameworkElement>);<xref:System.AddIn.Contract.INativeHandleContract>是外接程序用户界面，可跨隔离边界传递的可远程处理表示形式。  
  
3.  然后再从外接程序的应用程序域中，传递<xref:System.Windows.FrameworkElement>打包为<xref:System.AddIn.Contract.INativeHandleContract>通过调用<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>。  
  
4.  之后传递到主机应用程序的应用程序域<xref:System.AddIn.Contract.INativeHandleContract>必须重新打包为<xref:System.Windows.FrameworkElement>通过调用<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A>。  
  
 如何<xref:System.AddIn.Contract.INativeHandleContract>， <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A>，和<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>使用取决于特定方案。 下面几节介绍每个编程模型的详细信息。  
  
<a name="ReturnUIFromAddInContract"></a>   
## <a name="add-in-returns-a-user-interface"></a>外接程序返回用户界面  
 有关外接程序返回到主机应用程序的 UI，需要以下项：  
  
1.  主机应用程序、 外接程序和管道必须创建，如.NET Framework 中所述[外接程序和扩展性](/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100))文档。  
  
2.  协定必须实现<xref:System.AddIn.Contract.IContract>并返回一个用户界面，该协定必须声明具有类型的返回值的方法<xref:System.AddIn.Contract.INativeHandleContract>。  
  
3.  外接程序与主机应用程序之间传递 UI 必须直接或间接派生自<xref:System.Windows.FrameworkElement>。  
  
4.  必须从转换返回的外接程序的 UI<xref:System.Windows.FrameworkElement>到<xref:System.AddIn.Contract.INativeHandleContract>之前跨越隔离边界。  
  
5.  必须从转换返回 UI<xref:System.AddIn.Contract.INativeHandleContract>到<xref:System.Windows.FrameworkElement>后跨越隔离边界。  
  
6.  主机应用程序显示返回<xref:System.Windows.FrameworkElement>。  
  
 有关演示如何实现返回 UI 的外接程序示例，请参阅[创建外接程序返回 UI](how-to-create-an-add-in-that-returns-a-ui.md)。  
  
<a name="AddInIsAUI"></a>   
## <a name="add-in-is-a-user-interface"></a>外接程序为用户界面  
 当外接程序是一个 UI 时，具备以下条件：  
  
1.  主机应用程序、 外接程序和管道必须创建，如.NET Framework 中所述[外接程序和扩展性](/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100))文档。  
  
2.  外接程序的协定接口必须实现<xref:System.AddIn.Contract.INativeHandleContract>。  
  
3.  传递到主机应用程序的外接程序必须直接或间接派生自<xref:System.Windows.FrameworkElement>。  
  
4.  外接程序必须从转换<xref:System.Windows.FrameworkElement>到<xref:System.AddIn.Contract.INativeHandleContract>之前跨越隔离边界。  
  
5.  外接程序必须从转换<xref:System.AddIn.Contract.INativeHandleContract>到<xref:System.Windows.FrameworkElement>后跨越隔离边界。  
  
6.  主机应用程序显示返回<xref:System.Windows.FrameworkElement>。  
  
 有关演示如何实现作为 ui 的外接程序示例，请参阅[外接程序，它是创建 UI](how-to-create-an-add-in-that-is-a-ui.md)。  
  
<a name="ReturningMultipleUIsFromAnAddIn"></a>   
## <a name="returning-multiple-uis-from-an-add-in"></a>从外接程序返回多个 UI  
 外接程序通常提供多个主机应用程序显示用户界面。 例如，考虑为用户界面还提供状态信息到主机应用程序，也可用作 UI 的外接程序。 此类外接程序可以通过结合使用[外接程序返回用户界面](#ReturnUIFromAddInContract)和[外接程序为用户界面](#AddInIsAUI)模型中的技术来实现。  
  
<a name="AddInsAndXBAPs"></a>   
## <a name="add-ins-and-xaml-browser-applications"></a>外接程序和 XAML 浏览器应用程序  
 到目前为止，示例中的主机应用程序都安装为独立应用程序。 但是，如果满足以下附加的生成和实现要求，[!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)] 也可以承载外接程序：  
  
-   必须专门配置 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 应用程序清单，以便将管道（文件夹和程序集）和外接程序程序集下载到客户端计算机上的 [!INCLUDE[TLA#tla_clickonce](../../../../includes/tlasharptla-clickonce-md.md)] 应用程序缓存中 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 所在的文件夹中。  
  
-   用于发现和加载外接程序的 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 代码必须将 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 的 [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] 应用程序缓存用作管道和外接程序位置。  
  
-   如果外接程序引用位于源站点的松散文件，则 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 必须将外接程序加载到专门的安全上下文中；在由 [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] 承载时，外接程序只能引用位于主机应用程序源站点的松散文件。  
  
 下面几个小节将详细介绍这些任务。  
  
### <a name="configuring-the-pipeline-and-add-in-for-clickonce-deployment"></a>配置用于 ClickOnce 部署的管道和外接程序  
 [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] 将下载到 [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] 部署缓存中的安全文件夹并从该文件夹运行。 为了使 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 能够承载外接程序，还必须将管道和外接程序程序集下载到该安全文件夹。 为此，需要将应用程序清单配置为包含要下载的管道和外接程序程序集。 这在 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] 中最容易实现，但为使 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] 检测到管道程序集，管道和外接程序程序集需要位于宿主 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 项目的根文件夹中。  
  
 因此，第一步是通过设置每个管道程序集和外接程序程序集项目的生成输出，向 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 项目的根文件夹生成管道和外接程序程序集。 下表显示管道程序集项目和外接程序程序集项目的生成输出路径，这些路径位于与宿主 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 项目相同的解决方案和根文件夹中。  
  
 表 1:XBAP 承载的管道程序集生成输出路径  
  
|管道程序集项目|生成输出路径|  
|-------------------------------|-----------------------|  
|协定|`..\HostXBAP\Contracts\`|  
|加载项视图|`..\HostXBAP\AddInViews\`|  
|加载项方适配器|`..\HostXBAP\AddInSideAdapters\`|  
|宿主端适配器|`..\HostXBAP\HostSideAdapters\`|  
|外接程序|`..\HostXBAP\AddIns\WPFAddIn1`|  
  
 下一步是通过在 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] 中执行以下操作，将管道程序集和外接程序程序集指定为 [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] 内容文件：  
  
1.  通过在“解决方案资源管理器”中右键单击每个管道文件夹，然后选择“包括在项目中”，将管道和外接程序程序集包括在项目中。  
  
2.  在“属性”窗口中，将每个管道程序集和外接程序程序集的“生成操作”都设置为“内容”。  
  
 最后一步是配置应用程序清单，以包含要下载的管道程序集文件和外接程序程序集文件。 这些文件应位于 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 应用程序所占用的 [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] 缓存的根文件夹下的文件夹中。 通过执行以下操作，可以在 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] 中实现该配置：  
  
1.  右键单击 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 项目，依次单击“属性”、“发布”，然后单击“应用程序文件”按钮。  
  
2.  在“应用程序文件”对话框中，将每个管道和外接程序 DLL 的“发布状态”都设置为“包括(自动)”，并将每个管道和外接程序 DLL 的“下载组”都设置为“(必需)”。  
  
### <a name="using-the-pipeline-and-add-in-from-the-application-base"></a>从应用程序基使用管道和外接程序  
 为 [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] 部署配置管道和外接程序时，它们将下载到 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 所在的 [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] 缓存文件夹中。 若要从 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 中使用管道和外接程序，[!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 代码必须从应用程序基获取它们。 各种视频类型和模型使用的管道和外接程序的.NET Framework 外接程序的成员对于此方案提供特殊支持。 首先，路径由<xref:System.AddIn.Hosting.PipelineStoreLocation.ApplicationBase>枚举值。 将此值用于使用管道的相关外接程序成员的重载，这些成员包括：  
  
-   <xref:System.AddIn.Hosting.AddInStore.FindAddIns%28System.Type%2CSystem.AddIn.Hosting.PipelineStoreLocation%29?displayProperty=nameWithType>  
  
-   <xref:System.AddIn.Hosting.AddInStore.FindAddIns%28System.Type%2CSystem.AddIn.Hosting.PipelineStoreLocation%2CSystem.String%5B%5D%29?displayProperty=nameWithType>  
  
-   <xref:System.AddIn.Hosting.AddInStore.Rebuild%28System.AddIn.Hosting.PipelineStoreLocation%29?displayProperty=nameWithType>  
  
-   <xref:System.AddIn.Hosting.AddInStore.Update%28System.AddIn.Hosting.PipelineStoreLocation%29?displayProperty=nameWithType>  
  
### <a name="accessing-the-hosts-site-of-origin"></a>访问宿主的源站点  
 为确保外接程序可以引用源站点的文件，必须使用等效于主机应用程序的安全隔离来加载外接程序。 此安全级别由<xref:System.AddIn.Hosting.AddInSecurityLevel.Host?displayProperty=nameWithType>枚举值，并传递给<xref:System.AddIn.Hosting.AddInToken.Activate%2A>方法激活外接程序时。  
  
<a name="WPFAddInModelArchitecture"></a>   
## <a name="wpf-add-in-architecture"></a>WPF 外接程序体系结构  
 在最高级别，如我们所见，WPF 使.NET Framework 外接程序来实现用户界面 (的直接或间接派生<xref:System.Windows.FrameworkElement>) 使用<xref:System.AddIn.Contract.INativeHandleContract>，<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>和<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A>。 结果是，所以宿主应用程序将返回<xref:System.Windows.FrameworkElement>UI 中显示主机应用程序中。  
  
 对于简单 UI 外接程序的方案，这是开发人员需要尽可能详细。 对于更复杂的方案，特别是那些尝试使用其他 WPF 服务，如布局、 资源和数据绑定，更深入的了解 WPF 如何扩展模型的 UI 支持.NET Framework 外接程序的需要了解它的好处和限制。  
  
 从根本上说，WPF 未通过 UI 从外接程序的宿主应用程序;相反，WPF 将传递的 Win32 窗口句柄的 ui 使用 WPF 互操作性。 在这种情况下，当从外接程序的 UI 传递到主机应用程序时，将发生以下情况：  
  
-   在外接程序端，WPF 主机应用程序将显示的 ui 获取窗口句柄。 由派生的内部 WPF 类封装窗口句柄<xref:System.Windows.Interop.HwndSource>并实现<xref:System.AddIn.Contract.INativeHandleContract>。 此类的实例返回的<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>和从外接程序的应用程序域封至主机应用程序的应用程序域。  
  
-   在主机应用程序端，WPF 会重新打包<xref:System.Windows.Interop.HwndSource>作为内部 WPF 类派生自<xref:System.Windows.Interop.HwndHost>，并在使用<xref:System.AddIn.Contract.INativeHandleContract>。 此类的实例返回的<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A>到主机应用程序。  
  
 <xref:System.Windows.Interop.HwndHost> 存在能够显示用户界面，标识的窗口句柄，从 WPF 用户界面。 有关详细信息，请参阅 [WPF 和 Win32 互操作](../advanced/wpf-and-win32-interoperation.md)。  
  
 总之， <xref:System.AddIn.Contract.INativeHandleContract>， <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>，并<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A>存在的目的在于允许传递从外接程序的宿主应用程序中，通过封装了一个 WPF UI 的窗口句柄<xref:System.Windows.Interop.HwndHost>和显示主机应用程序的 UI。  
  
> [!NOTE]
>  由于主机应用程序获取<xref:System.Windows.Interop.HwndHost>，主机应用程序无法将返回的对象转换<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A>实现的类型它是通过外接程序 (例如， <xref:System.Windows.Controls.UserControl>)。  
  
 按其性质<xref:System.Windows.Interop.HwndHost>有某些限制，会影响主机应用程序可以使用它们。 但是，扩展了 WPF<xref:System.Windows.Interop.HwndHost>具备多个功能的外接程序方案。 下面介绍这些优点和限制。  
  
<a name="WPFAddInModelBenefits"></a>   
## <a name="wpf-add-in-benefits"></a>WPF 外接程序的优点  
 由于 WPF 外接程序用户界面显示从主机应用程序使用的内部类派生自<xref:System.Windows.Interop.HwndHost>，这些用户界面的功能受到<xref:System.Windows.Interop.HwndHost>方面布局，如 WPF UI 服务呈现、 数据绑定、 样式、 模板和资源。 但是，WPF 扩展了其内部<xref:System.Windows.Interop.HwndHost>子类的附加功能，包括以下：  
  
-   主机应用程序的 UI 和外接程序的 UI 之间按 tab 键。 请注意，"外接程序是一个用户界面"编程模型需要外接程序端适配器重写<xref:System.AddIn.Pipeline.ContractBase.QueryContract%2A>使 tab 键切换功能，无论外接程序是完全信任还是部分受信任的。  
  
-   接受从主机应用程序的用户界面显示的外接程序用户界面的可访问性要求。  
  
-   使 WPF 应用程序能够在多个应用程序域方案中安全地运行。  
  
-   防止非法访问外接程序用户界面窗口句柄时使用安全隔离 （即，部分信任安全沙盒） 运行外接程序。 调用<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>以确保此安全性：  
  
    -   对于"外接程序返回 UI"编程模型的一个外接程序的 UI 跨隔离边界传递的窗口句柄的唯一方法是调用<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>。  
  
    -   对于"外接程序是一个用户界面"的编程模型，重写<xref:System.AddIn.Pipeline.ContractBase.QueryContract%2A>上的外接程序端适配器和调用<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>（如上述示例中所示） 是必需的因为调用外接程序端适配器`QueryContract`实现主机端适配器。  
  
-   提供多个应用程序域执行保护。 由于应用程序域的限制，因此即使存在隔离边界，外接程序应用程序域中引发的未经处理的异常也会导致整个应用程序出现故障。 但是，WPF 和.NET Framework 外接程序模型提供简单的方法要解决此问题并提高应用程序的稳定性。 WPF 外接程序显示的 UI 创建<xref:System.Windows.Threading.Dispatcher>的线程的应用程序域在上运行，如果主机应用程序是一个 WPF 应用程序。 你可以检测到处理应用程序域中发生的所有未处理的异常<xref:System.Windows.Threading.Dispatcher.UnhandledException>WPF 外接程序的事件<xref:System.Windows.Threading.Dispatcher>。 可以获取<xref:System.Windows.Threading.Dispatcher>从<xref:System.Windows.Threading.Dispatcher.CurrentDispatcher%2A>属性。  
  
<a name="WPFAddInModelLimitations"></a>   
## <a name="wpf-add-in-limitations"></a>WPF 外接程序限制  
 WPF 将添加到由提供的默认行为的优点之外<xref:System.Windows.Interop.HwndSource>， <xref:System.Windows.Interop.HwndHost>，和窗口句柄，也有限制从主机应用程序显示的外接程序用户界面：  
  
-   从主机应用程序中显示的外接程序用户界面不遵从主机应用程序的剪辑行为。  
  
-   互操作性方案中的“空域”概念也适用于外接程序（请参阅[技术区概述](../advanced/technology-regions-overview.md)）。  
  
-   主机应用程序的 UI 服务，如资源继承、 数据绑定和命令，不会自动提供外接程序用户界面。 若要向外接程序提供这些服务，需要更新管道。  
  
-   不能旋转、 缩放、 倾斜，或不受转换一个外接程序的 UI (请参阅[转换概述](../graphics-multimedia/transforms-overview.md))。  
  
-   通过绘制从操作呈现的外接程序用户界面中的内容<xref:System.Drawing>命名空间可以包含 alpha 值混合处理。 但是，加载项 UI 和主机应用程序 UI，其中包含它必须是 100%不透明的;换而言之，`Opacity`上的属性必须设置为 1。  
  
-   如果<xref:System.Windows.Window.AllowsTransparency%2A>窗口包含一个外接程序的 UI 在主机应用程序中的属性设置为`true`外, 接程序是不可见。 即使外接程序用户界面是 100%不透明，这是如此 (即，`Opacity`属性具有值为 1)。  
  
-   加载项 UI 必须出现在同一顶级窗口中的其他 WPF 元素之上。  
  
-   可以使用呈现外接程序的 UI 的任何部分<xref:System.Windows.Media.VisualBrush>。 相反外, 接程序可能需要生成用户界面中，若要创建位图，可传递到主机应用程序使用通过协定所定义的方法的快照。  
  
-   不能从播放媒体文件<xref:System.Windows.Controls.MediaElement>外接程序 UI 中。  
  
-   生成外接程序用户界面的鼠标事件则既不接收，也不引发主机应用程序，并`IsMouseOver`主机应用程序 UI 的属性的值为`false`。  
  
-   当外接程序 UI 中的控件焦点`GotFocus`和`LostFocus`事件是既没有接收到不会引发主机应用程序。  
  
-   包含一个外接程序的 UI 的主机应用程序的部分将显示为空白时打印。  
  
-   所有调度程序 (请参阅<xref:System.Windows.Threading.Dispatcher>) 由外接程序创建 UI 必须手动关闭所有者外接程序卸载之前如果主机应用程序继续执行。 协定可以实现允许主机应用程序外接程序卸载之前通知外接程序，从而允许外接程序用户界面关闭自己的调度程序的方法。  
  
-   如果加载项 UI<xref:System.Windows.Controls.InkCanvas>或包含<xref:System.Windows.Controls.InkCanvas>，不能卸载外接程序。  
  
<a name="PerformanceOptimization"></a>   
## <a name="performance-optimization"></a>性能优化  
 默认情况下，当使用多个应用程序域时，每个应用程序所需的各种.NET Framework 程序集是所有加载到该应用程序的域。 因此，创建新应用程序域和在应用程序域中启动应用程序所需的时间可能会影响性能。 但是，.NET Framework 提供了一种方法，从而减少启动时间即指示应用程序在应用程序域之间共享程序集，如果他们已加载。 执行此操作通过使用<xref:System.LoaderOptimizationAttribute>属性，必须应用于入口点方法 (`Main`)。 这种情况下，只能使用代码来实现应用程序定义（请参阅[应用程序管理概述](application-management-overview.md)）。  
  
## <a name="see-also"></a>请参阅
- <xref:System.LoaderOptimizationAttribute>
- [外接程序和扩展性](/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100))
- [应用程序域](../../app-domains/application-domains.md)
- [.NET framework 远程处理概述](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/kwdt6w2k(v=vs.100))
- [使对象可远程处理](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/wcf3swha(v=vs.100))
- [帮助主题](how-to-topics.md)
