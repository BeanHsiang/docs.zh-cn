---
title: 如何：同步定位时钟
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- clocks [WPF], seeking synchronously
- seeking clocks synchronously [WPF]
ms.assetid: e5b7529b-b7d0-40d2-9e1d-fa4b5e736e96
ms.openlocfilehash: 9b6b1f5523effc56ccd9ddaa4f478e1d3a20ada8
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57355983"
---
# <a name="how-to-seek-a-clock-synchronously"></a>如何：同步定位时钟
使用<xref:System.Windows.Media.Animation.ClockController.SeekAlignedToLastTick%2A>方法来同步定位时钟的特定点。 下面的示例演示<xref:System.Windows.Media.Animation.ClockController.Seek%2A>并<xref:System.Windows.Media.Animation.ClockController.SeekAlignedToLastTick%2A>方法的<xref:System.Windows.Media.Animation.ClockController>。  
  
 此示例演示如何查找<xref:System.Windows.Media.Animation.Clock>; 对于一个示例，演示如何搜寻演示图板，请参阅[情节提要同步搜寻](how-to-seek-a-storyboard-synchronously.md)。  
  
## <a name="example"></a>示例  
 [!code-csharp[ClockController_procedural_snip#ClockControllerSeekExample](~/samples/snippets/csharp/VS_Snippets_Wpf/ClockController_procedural_snip/CSharp/SeekAlignedToLastTickExample.cs#clockcontrollerseekexample)]
 [!code-vb[ClockController_procedural_snip#ClockControllerSeekExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ClockController_procedural_snip/visualbasic/seekalignedtolasttickexample.vb#clockcontrollerseekexample)]
