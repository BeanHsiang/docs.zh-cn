---
title: 如何：手动管理缓冲的图形
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- flicker [Windows Forms], reducing by manually managing graphics
- graphics [Windows Forms], managing buffered
ms.assetid: 4c2a90ee-bbbe-4ff6-9170-1b06c195c918
ms.openlocfilehash: 013118ea15184ee4dfbbcd5dcaff054a2cf6a9ba
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57702927"
---
# <a name="how-to-manually-manage-buffered-graphics"></a>如何：手动管理缓冲的图形
对于更高级的双缓冲方案，可以使用[!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]类以实现您自己的双缓冲逻辑。 负责分配和管理各个图形缓冲的类是<xref:System.Drawing.BufferedGraphicsContext>类。 每个应用程序具有自己的默认<xref:System.Drawing.BufferedGraphicsContext>管理所有默认双缓冲该应用程序。 可以通过调用检索到此实例的引用<xref:System.Drawing.BufferedGraphicsManager.Current%2A>。  
  
### <a name="to-obtain-a-reference-to-the-default-bufferedgraphicscontext"></a>若要获取对默认 BufferedGraphicsContext 的引用  
  
-   设置<xref:System.Drawing.BufferedGraphicsManager.Current%2A>属性，如下面的代码示例中所示。  
  
     [!code-csharp[System.Windows.Forms.LegacyBufferedGraphics#11](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/CS/Class1.cs#11)]
     [!code-vb[System.Windows.Forms.LegacyBufferedGraphics#11](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/VB/Class1.vb#11)]  
  
    > [!NOTE]
    >  不需要调用`Dispose`方法<xref:System.Drawing.BufferedGraphicsContext>引用接收来自<xref:System.Drawing.BufferedGraphicsManager>类。 <xref:System.Drawing.BufferedGraphicsManager>处理的所有内存分配和默认值的分布<xref:System.Drawing.BufferedGraphicsContext>实例。  
  
     如动画图形密集型应用程序，您有时可以提高性能使用的专用<xref:System.Drawing.BufferedGraphicsContext>而不是<xref:System.Drawing.BufferedGraphicsContext>提供的<xref:System.Drawing.BufferedGraphicsManager>。 这使您可以创建和管理图形缓冲区单独，而不会产生管理所有其他缓冲的图形与应用程序关联，但应用程序所占用的内存将更大的性能开销。  
  
### <a name="to-create-a-dedicated-bufferedgraphicscontext"></a>若要创建专用的 BufferedGraphicsContext  
  
-   声明和创建的新实例<xref:System.Drawing.BufferedGraphicsContext>类，如下面的代码示例中所示。  
  
     [!code-csharp[System.Windows.Forms.LegacyBufferedGraphics#12](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/CS/Class1.cs#12)]
     [!code-vb[System.Windows.Forms.LegacyBufferedGraphics#12](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/VB/Class1.vb#12)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Drawing.BufferedGraphicsContext>
- [双缓冲的图形](double-buffered-graphics.md)
- [如何：手动呈现缓冲的图形](how-to-manually-render-buffered-graphics.md)
