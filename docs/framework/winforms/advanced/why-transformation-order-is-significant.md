---
title: 为什么转换顺序非常重要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- transformations [Windows Forms], order significance
ms.assetid: 37d5f9dc-a5cf-4475-aa5d-34d714e808a9
ms.openlocfilehash: 4a65e588984241affea3083810b4901266480ea4
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57710380"
---
# <a name="why-transformation-order-is-significant"></a>为什么转换顺序非常重要
单个<xref:System.Drawing.Drawing2D.Matrix>对象可以存储的单个转换的序列。 后一种称为复合转换。 复合转换矩阵被获取的单个转换的矩阵相乘。  
  
## <a name="composite-transform-examples"></a>复合转换示例  
 在复合转换中，各个转换的顺序非常重要。 例如，如果首先旋转，然后扩展，然后转换，您获得不同的结果不是如果首先将旋转，则缩放。 在[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)]，复合转换是从左到右。 如果 S、 R 和 T 分别为缩放、 旋转和转换矩阵，然后产品 （按此顺序） SRT 是扩展的第一的复合转换的矩阵，旋转，然后将转换。 生成的产品的矩阵 SRT 为不同于生成的乘积 TRS 矩阵。  
  
 顺序很重要的原因之一是，这样针对的坐标系的原点的像旋转和缩放的变换。 缩放以原点为中心的对象生成不同的结果已离开源的对象与缩放。 同样，旋转以原点为中心的对象生成不同的结果比旋转对象已移动背离原点。  
  
 下面的示例结合缩放、 旋转和平移 （按照该顺序） 以形成的复合转换。 自变量<xref:System.Drawing.Drawing2D.MatrixOrder.Append>传递给<xref:System.Drawing.Graphics.RotateTransform%2A>方法指示旋转将遵循的缩放。 同样，参数<xref:System.Drawing.Drawing2D.MatrixOrder.Append>传递给<xref:System.Drawing.Graphics.TranslateTransform%2A>方法指示翻译将遵循旋转。 <xref:System.Drawing.Drawing2D.MatrixOrder.Append> 并<xref:System.Drawing.Drawing2D.MatrixOrder.Prepend>成员的<xref:System.Drawing.Drawing2D.MatrixOrder>枚举。  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#21](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.MiscLegacyTopics#21](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#21)]  
  
 下面的示例可以相同的方法调用与上面的示例中，但调用的顺序相反。 操作的结果的顺序平移、 然后旋转和缩放，即会生成非常不同的结果比第一个刻度，然后将旋转，然后转换。  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#22](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#22)]
 [!code-vb[System.Drawing.MiscLegacyTopics#22](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#22)]  
  
 若要反转的复合转换中的单个转换顺序的一种方法是反转的一系列方法调用的顺序。 控制操作的顺序的第二个方法是更改矩阵 order 参数。 下面的示例等同于上述示例中，不同之处在于<xref:System.Drawing.Drawing2D.MatrixOrder.Append>已更改为<xref:System.Drawing.Drawing2D.MatrixOrder.Prepend>。 矩阵乘法是按顺序完成的 SRT，S、 R 和 T 是缩放、 旋转的矩阵和分别转换。 复合转换的顺序是第一个刻度，然后旋转，然后转换。  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#23](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#23)]
 [!code-vb[System.Drawing.MiscLegacyTopics#23](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#23)]  
  
 立即前面中的结果是示例的相同作为本主题中的第一个示例的结果。 这是因为我们颠倒方法调用的顺序和矩阵乘法的顺序。  
  
## <a name="see-also"></a>请参阅

- <xref:System.Drawing.Drawing2D.Matrix>
- [坐标系统和转换](coordinate-systems-and-transformations.md)
- [在托管 GDI+ 中使用转换](using-transformations-in-managed-gdi.md)
