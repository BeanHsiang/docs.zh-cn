---
title: 多媒体概述
ms.date: 03/30/2017
helpviewer_keywords:
- multimedia [WPF]
- media [WPF]
ms.assetid: feb25b15-d741-4ac3-818f-1b19f63a3562
ms.openlocfilehash: 09b830562444bd51e931a1b5013d2a803319e336
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57352759"
---
# <a name="multimedia-overview"></a>多媒体概述
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中的多媒体功能能够使音频和视频集成到应用程序，增强用户体验。 本主题介绍了 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的多媒体功能。  
  
 
  
<a name="mediaapi"></a>   
## <a name="media-api"></a>媒体 API  
 <xref:System.Windows.Controls.MediaElement>和<xref:System.Windows.Media.MediaPlayer>类用于提供音频或视频内容。 可以以交互方式或时钟控制这些类。 这些类可以用在 [!INCLUDE[TLA#tla_wmp](../../../../includes/tlasharptla-wmp-md.md)] 10 控件上进行媒体播放。 要使用哪个类取决于方案。  
  
 <xref:System.Windows.Controls.MediaElement> 是<xref:System.Windows.UIElement>受[布局](../advanced/layout.md)并且可用作许多控件的内容。 它也可用在 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 与代码中。 <xref:System.Windows.Media.MediaPlayer>但是，专为<xref:System.Windows.Media.Drawing>对象，因而缺少布局支持。 加载使用介质<xref:System.Windows.Media.MediaPlayer>仅可以使用呈现<xref:System.Windows.Media.VideoDrawing>或通过直接与交互<xref:System.Windows.Media.DrawingContext>。 <xref:System.Windows.Media.MediaPlayer> 不能在 XAML 中使用。  
  
 有关绘图对象和绘图上下文的详细信息，请参阅 [Drawing 对象概述](drawing-objects-overview.md)。  
  
> [!NOTE]
>  使用应用程序分发媒体时，不可将媒体文件用作项目资源。 在项目文件中，必须改为将媒体类型设置为 `Content` 并将 `CopyToOutputDirectory` 设置为 `PreserveNewest` 或 `Always`。  
  
<a name="mediaplaybackmodes"></a>   
## <a name="media-playback-modes"></a>媒体播放模式  
  
> [!NOTE]
>  这两<xref:System.Windows.Controls.MediaElement>和<xref:System.Windows.Media.MediaPlayer>拥有相似的成员。 在本部分链接是指<xref:System.Windows.Controls.MediaElement>类成员。 除非特别注明，否则成员链接到在<xref:System.Windows.Controls.MediaElement>类还可在<xref:System.Windows.Media.MediaPlayer>类。  
  
 要了解 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中的媒体播放，需要了解可以播放媒体的不同模式。 这两<xref:System.Windows.Controls.MediaElement>和<xref:System.Windows.Media.MediaPlayer>可在两个不同的媒体模式，独立模式和时钟模式。 媒体模式由<xref:System.Windows.Controls.MediaElement.Clock%2A>属性。 当<xref:System.Windows.Controls.MediaElement.Clock%2A>是`null`，媒体对象处于独立模式。 当<xref:System.Windows.Controls.MediaElement.Clock%2A>为非 null，媒体对象处于时钟模式。 默认情况下，媒体对象处于独立模式。  
  
### <a name="independent-mode"></a>独立模式  
 在独立模式下，媒体内容驱动媒体播放。 独立模式可实现下列选项：  
  
-   媒体的<xref:System.Uri>可以直接指定。  
  
-   可以直接控制媒体播放。  
  
-   媒体的<xref:System.Windows.Controls.MediaElement.Position%2A>和<xref:System.Windows.Controls.MediaElement.SpeedRatio%2A>可以修改属性。  
  
 通过这两个设置加载媒体<xref:System.Windows.Controls.MediaElement>对象的<xref:System.Windows.Controls.MediaElement.Source%2A>属性或通过调用<xref:System.Windows.Media.MediaPlayer>对象的<xref:System.Windows.Media.MediaPlayer.Open%2A>方法。  
  
 要在独立模式下控制媒体播放，可使用媒体对象的控制方法。 可用的控制方法都<xref:System.Windows.Controls.MediaElement.Play%2A>， <xref:System.Windows.Controls.MediaElement.Pause%2A>， <xref:System.Windows.Controls.MediaElement.Close%2A>，和<xref:System.Windows.Controls.MediaElement.Stop%2A>。 有关<xref:System.Windows.Controls.MediaElement>，使用这些方法的交互式控件才可用<xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A>设置为<xref:System.Windows.Controls.MediaState.Manual>。 这些方法在媒体对象处于时钟模式时不可用。  
  
 请参阅[控制 MediaElement（Play、Pause、Stop、Volume 和 Speed）](how-to-control-a-mediaelement-play-pause-stop-volume-and-speed.md)了解独立模式的示例。  
  
### <a name="clock-mode"></a>时钟模式  
 在时钟模式下，<xref:System.Windows.Media.MediaTimeline>驱动器媒体的播放。 时钟模式具有以下特征：  
  
-   媒体的<xref:System.Uri>间接设置通过<xref:System.Windows.Media.MediaTimeline>。  
  
-   可由时钟控制媒体播放。 不可使用媒体对象的控制方法。  
  
-   通过设置加载介质<xref:System.Windows.Media.MediaTimeline>对象的<xref:System.Windows.Media.MediaTimeline.Source%2A>属性，从时间线创建时钟并将时钟分配至媒体对象。 这种方法还加载媒体时<xref:System.Windows.Media.MediaTimeline>内<xref:System.Windows.Media.Animation.Storyboard>目标<xref:System.Windows.Controls.MediaElement>。  
  
 在时钟模式下控制媒体播放<xref:System.Windows.Media.Animation.ClockController>必须使用控制方法。 一个<xref:System.Windows.Media.Animation.ClockController>取自<xref:System.Windows.Media.Animation.ClockController>属性的<xref:System.Windows.Media.MediaClock>。 如果尝试使用的控制方法<xref:System.Windows.Controls.MediaElement>或<xref:System.Windows.Media.MediaPlayer>对象在时钟模式下，<xref:System.InvalidOperationException>将引发。  
  
 请参阅[动画概述](animation-overview.md)了解有关时钟和时间线的更多信息。  
  
 请参阅[使用情节提要控制 MediaElement](how-to-control-a-mediaelement-by-using-a-storyboard.md) 了解时钟模式的示例。  
  
<a name="mediaelement"></a>   
## <a name="mediaelement-class"></a>MediaElement 类  
 将媒体添加到应用程序非常简单，添加<xref:System.Windows.Controls.MediaElement>控制对[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]的应用程序，并提供<xref:System.Uri>到你想要包括的媒体。 所有 [!INCLUDE[TLA#tla_wmp](../../../../includes/tlasharptla-wmp-md.md)] 10 支持的媒体类型都受到 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 的支持。 下面的示例演示的简单用法<xref:System.Windows.Controls.MediaElement>在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]。  
  
 [!code-xaml[MediaElement_snip#SimpleMediaElementUsageWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/MediaElement_snip/CSharp/SimpleUsage.xaml#simplemediaelementusagewholepage)]  
  
 在此示例中，媒体一旦加载会自动播放。 媒体完成播放后会关闭并且所有媒体资源已发布（包括视频内存）。 这是默认行为<xref:System.Windows.Controls.MediaElement>对象，并由控制<xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A>和<xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A>属性。  
  
### <a name="controlling-a-mediaelement"></a>控制 MediaElement  
 <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A>并<xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A>属性控制的行为<xref:System.Windows.Controls.MediaElement>时<xref:System.Windows.FrameworkElement.IsLoaded%2A>是`true`或`false`分别。 <xref:System.Windows.Controls.MediaState>的属性设置为影响媒体播放行为。 例如，默认值<xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A>是<xref:System.Windows.Controls.MediaState.Play>和默认<xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A>是<xref:System.Windows.Controls.MediaState.Close>。 这意味着，只要<xref:System.Windows.Controls.MediaElement>加载和预滚完成，媒体开始播放。 一旦播放完毕，媒体就会关闭并且发布所有媒体资源。  
  
 <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A>和<xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A>属性不是控制媒体播放的唯一方法。 在时钟模式下，可以控制时钟<xref:System.Windows.Controls.MediaElement>和交互式控制方法具有控制何时<xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A>是<xref:System.Windows.Controls.MediaState.Manual>。 <xref:System.Windows.Controls.MediaElement> 通过评估以下属性来处理这种控制争用。  
  
1.  <xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A>。 卸载媒体时就位。 这可确保默认情况下，会释放所有的媒体资源，即使<xref:System.Windows.Media.MediaClock>与关联<xref:System.Windows.Controls.MediaElement>。  
  
2.  <xref:System.Windows.Media.MediaClock>。 在媒体具有时就位<xref:System.Windows.Controls.MediaElement.Clock%2A>。 如果媒体已卸载，<xref:System.Windows.Media.MediaClock>将会生效，只要<xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A>是<xref:System.Windows.Controls.MediaState.Manual>。 时钟模式下将始终覆盖的加载的行为<xref:System.Windows.Controls.MediaElement>。  
  
3.  <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A>。 加载媒体时就位。  
  
4.  交互式控制方法。 在发生<xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A>是<xref:System.Windows.Controls.MediaState.Manual>。 可用的控制方法都<xref:System.Windows.Controls.MediaElement.Play%2A>， <xref:System.Windows.Controls.MediaElement.Pause%2A>， <xref:System.Windows.Controls.MediaElement.Close%2A>，和<xref:System.Windows.Controls.MediaElement.Stop%2A>。  
  
### <a name="displaying-a-mediaelement"></a>显示 MediaElement  
 若要显示<xref:System.Windows.Controls.MediaElement>它必须具有要呈现的内容，其中包含其<xref:System.Windows.FrameworkElement.ActualWidth%2A>和<xref:System.Windows.FrameworkElement.ActualHeight%2A>属性设置为零，直到加载内容。 对于仅包含音频的内容，这些属性将始终为零。 有关视频内容，一次<xref:System.Windows.Controls.MediaElement.MediaOpened>引发事件<xref:System.Windows.FrameworkElement.ActualWidth%2A>和<xref:System.Windows.FrameworkElement.ActualHeight%2A>将报表加载媒体的大小。 这意味着，媒体已加载，直到<xref:System.Windows.Controls.MediaElement>不会占用任何物理空间[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]除非<xref:System.Windows.FrameworkElement.Width%2A>或<xref:System.Windows.FrameworkElement.Height%2A>设置属性。  
  
 将两者都设置<xref:System.Windows.FrameworkElement.Width%2A>并<xref:System.Windows.FrameworkElement.Height%2A>属性会导致媒体拉伸以填充为提供的区域<xref:System.Windows.Controls.MediaElement>。 若要保留媒体的原始纵横比，或者<xref:System.Windows.FrameworkElement.Width%2A>或<xref:System.Windows.FrameworkElement.Height%2A>属性应设置好，但不可同时使用两者。 将两者都设置<xref:System.Windows.FrameworkElement.Width%2A>和<xref:System.Windows.FrameworkElement.Height%2A>属性会导致媒体以固定的元素大小，您可能希望呈现。  
  
 要避免出现固定大小元素，[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 可以预滚媒体。 这是通过设置<xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A>至任一<xref:System.Windows.Controls.MediaState.Play>或<xref:System.Windows.Controls.MediaState.Pause>。 在<xref:System.Windows.Controls.MediaState.Pause>状态下，媒体会预播放，将显示第一个帧。 在<xref:System.Windows.Controls.MediaState.Play>状态时，媒体将预滚并开始播放。  
  
<a name="mediaplayer"></a>   
## <a name="mediaplayer-class"></a>MediaPlayer 类  
 作为 where<xref:System.Windows.Controls.MediaElement>类是框架元素，其<xref:System.Windows.Media.MediaPlayer>类旨在用于<xref:System.Windows.Media.Drawing>对象。 当可以牺牲框架级别功能来获得性能优势，或在需要时使用 drawing 对象<xref:System.Windows.Freezable>功能。 <xref:System.Windows.Media.MediaPlayer> 可以充分利用这些功能，同时提供你的应用程序中的媒体内容。 像<xref:System.Windows.Controls.MediaElement>，<xref:System.Windows.Media.MediaPlayer>可在独立或时钟模式，但不是会不具有<xref:System.Windows.Controls.MediaElement>对象的卸载和加载状态。 这会减少播放控件的复杂程度<xref:System.Windows.Media.MediaPlayer>。  
  
### <a name="controlling-mediaplayer"></a>控制 MediaPlayer  
 因为<xref:System.Windows.Media.MediaPlayer>是无状态的有只有两个方法控制媒体的播放。  
  
1.  交互式控制方法。 在处于独立模式下时的位置 (`null` <xref:System.Windows.Media.MediaPlayer.Clock%2A>属性)。  
  
2.  <xref:System.Windows.Media.MediaClock>。 在媒体具有时就位<xref:System.Windows.Media.MediaPlayer.Clock%2A>。  
  
### <a name="displaying-a-mediaplayer"></a>显示 MediaPlayer  
 从技术上讲，<xref:System.Windows.Media.MediaPlayer>无法显示，因为它必须没有物理表示形式。 但是，使用它来显示在媒体<xref:System.Windows.Media.Drawing>使用<xref:System.Windows.Media.VideoDrawing>类。 下面的示例演示如何将<xref:System.Windows.Media.VideoDrawing>显示媒体。  
  
 [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline)]  
  
 请参阅[Drawing 对象概述](drawing-objects-overview.md)有关详细信息<xref:System.Windows.Media.Drawing>对象。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Media.DrawingGroup>
- [布局](../advanced/layout.md)
- [帮助主题](audio-and-video-how-to-topics.md)
