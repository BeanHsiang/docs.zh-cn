---
title: 全局变换和局部变换
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- matrices [Windows Forms], using transformations
- transformations [Windows Forms], global
- transformations [Windows Forms], local
ms.assetid: b601d66d-d572-4f11-9d2e-92f0dc8893f3
ms.openlocfilehash: 07ef61e3a41448f051fb9b7da2cfd91d7cbf26b5
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57711845"
---
# <a name="global-and-local-transformations"></a>全局变换和局部变换
全局转换是适用于由绘制每个项的转换给定<xref:System.Drawing.Graphics>对象。 与此相反，本地转换是适用于特定项要绘制的转换。  
  
## <a name="global-transformations"></a>全局转换  
 若要创建全局转换，请构造<xref:System.Drawing.Graphics>对象，并处理其<xref:System.Drawing.Graphics.Transform%2A>属性。 <xref:System.Drawing.Graphics.Transform%2A>属性是<xref:System.Drawing.Drawing2D.Matrix>对象，因此它可以保存任何仿射转换的序列。 转换存储在<xref:System.Drawing.Graphics.Transform%2A>属性称为世界转换。 <xref:System.Drawing.Graphics>类提供了构建复合世界转换的几种方法： <xref:System.Drawing.Graphics.MultiplyTransform%2A>， <xref:System.Drawing.Graphics.RotateTransform%2A>， <xref:System.Drawing.Graphics.ScaleTransform%2A>，和<xref:System.Drawing.Graphics.TranslateTransform%2A>。 下面的示例绘制一个椭圆两次： 一次之前创建世界转换和之后的一次。 转换首先按 y 方向的 0.5 的比例缩放然后将为 50 个单位 x 方向，然后将旋转 30 度。  
  
 [!code-csharp[System.Drawing.CoordinateSystems#21](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.CoordinateSystems#21](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/VB/Class1.vb#21)]  
  
 下图显示矩阵涉及在转换中。  
  
 ![Transformations](./media/aboutgdip05-art14.gif "AboutGdip05_art14")  
  
> [!NOTE]
>  在前面的示例中，椭圆围绕位于工作区的左上角的坐标系的原点。 这将产生比旋转椭圆围绕其自身中心不同的结果。  
  
## <a name="local-transformations"></a>本地转换  
 本地转换应用到要绘制的特定项。 例如，<xref:System.Drawing.Drawing2D.GraphicsPath>对象具有<xref:System.Drawing.Drawing2D.GraphicsPath.Transform%2A>，可以将该路径的数据点的方法。 下面的示例绘制一个具有任何转换的矩形和具有旋转转换的路径。 （假定没有任何世界转换。）  
  
 [!code-csharp[System.Drawing.CoordinateSystems#22](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/CS/Class1.cs#22)]
 [!code-vb[System.Drawing.CoordinateSystems#22](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/VB/Class1.vb#22)]  
  
 你可以组合使用本地转换，以实现各种结果的世界转换。 例如，可以使用世界转换修改坐标系统，并使用本地转换来旋转和缩放新的坐标系统上绘制的对象。  
  
 假设您希望具有其源为 200 像素从工作区左边缘和从客户端区域的顶部 150 像素坐标系统。 此外，假定您需要的度量单位为像素，且 x 轴指向右，y 轴指向上方。 默认坐标系统具有 y 轴指向下方，因此您需要在水平轴上执行反射。 下图显示了此类反射的矩阵。  
  
 ![Transformations](./media/aboutgdip05-art15.gif "AboutGdip05_art15")  
  
 接下来，假定您需要执行转换 200 个单位的向右和向下的 150 个单位。  
  
 下面的示例建立刚刚介绍通过设置世界转换的坐标系统<xref:System.Drawing.Graphics>对象。  
  
 [!code-csharp[System.Drawing.CoordinateSystems#23](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/CS/Class1.cs#23)]
 [!code-vb[System.Drawing.CoordinateSystems#23](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/VB/Class1.vb#23)]  
  
 下面的代码 （放在上面的示例末尾） 创建包含新的坐标系统的原点位于其左下角的一个矩形的路径。 与任何本地转换和局部转换一次，一次填充矩形。 水平缩放到原来的 2 的 30 度旋转后跟包含本地转换。  
  
 [!code-csharp[System.Drawing.CoordinateSystems#24](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/CS/Class1.cs#24)]
 [!code-vb[System.Drawing.CoordinateSystems#24](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/VB/Class1.vb#24)]  
  
 下图显示了新的坐标系统和两个矩形。  
  
 ![Transformations](./media/aboutgdip05-art16.gif "AboutGdip05_art16")  
  
## <a name="see-also"></a>请参阅
- [坐标系统和转换](coordinate-systems-and-transformations.md)
- [在托管 GDI+ 中使用转换](using-transformations-in-managed-gdi.md)
