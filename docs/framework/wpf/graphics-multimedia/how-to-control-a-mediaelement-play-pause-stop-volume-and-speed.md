---
title: 如何：控制 MediaElement（播放、暂停、停止、音量和速度）
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- playback of media [WPF], controlling
- controlling playback of media [WPF]
- multimedia [WPF], controlling playback of media
- media [WPF], controlling playback of
ms.assetid: 6885a730-e054-4c16-8c1e-ffe17b1f7c32
ms.openlocfilehash: 7fe8107f7b5b65f00f2c5ac029f806aeba758d20
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57368501"
---
# <a name="how-to-control-a-mediaelement-play-pause-stop-volume-and-speed"></a>如何：控制 MediaElement（播放、暂停、停止、音量和速度）
下面的示例演示如何控制播放的媒体使用<xref:System.Windows.Controls.MediaElement>。 该示例创建简单的媒体播放器，可用于播放、 暂停、 停止，请跳过在媒体中的往返，以及调整音量和速度比。  
  
## <a name="example"></a>示例  
 以下代码创建 UI。  
  
> [!NOTE]
>  <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A>的属性<xref:System.Windows.Controls.MediaElement>必须设置为`Manual`以便能够以交互方式停止、 暂停和播放媒体。  
  
 [!code-xaml[MediaGallery_snip#MediaElementExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MediaGallery_snip/VB/MediaElementExample.xaml#mediaelementexamplewholepage)]  
  
## <a name="example"></a>示例  
 下面的代码实现的示例 UI 控件的功能。 <xref:System.Windows.Controls.MediaElement.Play%2A>， <xref:System.Windows.Controls.MediaElement.Pause%2A>，和<xref:System.Windows.Controls.MediaElement.Stop%2A>方法用于分别播放、 暂停和停止该媒体。 更改<xref:System.Windows.Controls.MediaElement.Position%2A>属性的<xref:System.Windows.Controls.MediaElement>可以跳过在媒体中。 最后，<xref:System.Windows.Controls.MediaElement.Volume%2A>和<xref:System.Windows.Controls.MediaElement.SpeedRatio%2A>属性用来调整媒体的音量和播放速度。  
  
 [!code-csharp[MediaGallery_snip#CodeBehindMediaElementExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/MediaGallery_snip/CSharp/MediaElementExample.xaml.cs#codebehindmediaelementexamplewholepage)]
 [!code-vb[MediaGallery_snip#CodeBehindMediaElementExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MediaGallery_snip/VB/MediaElementExample.xaml.vb#codebehindmediaelementexamplewholepage)]  
  
## <a name="see-also"></a>请参阅
- [使用情节提要控制 MediaElement](how-to-control-a-mediaelement-by-using-a-storyboard.md)
