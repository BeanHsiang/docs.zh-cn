---
title: 转换的矩阵表示形式
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- composite transformations
- transformations [Windows Forms], linear
- matrices
- translations in matrix representation
- transformations [Windows Forms], composite
- vectors
- linear transformations
- transformations [Windows Forms], matrix representation of
- transformations [Windows Forms], translation
- affine transformations
ms.assetid: 0659fe00-9e0c-41c4-9118-016f2404c905
ms.openlocfilehash: 1f98dac8b9d14cac01e109627d40fe01c37c6954
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57720821"
---
# <a name="matrix-representation-of-transformations"></a>转换的矩阵表示形式
M × n 矩阵是一组按 m 行和 n 列排列的数字。 下图显示了几个矩阵。  
  
 ![Transformations](./media/aboutgdip05-art04.gif "AboutGdip05_art04")  
  
 可以通过添加各个元素添加两个相同大小的矩阵。 下图显示矩阵添加两个的示例。  
  
 ![Transformations](./media/aboutgdip05-art05.gif "AboutGdip05_art05")  
  
 M × n 矩阵可以是 n × p 的矩阵相乘，并且结果为 m × p 矩阵。 中的第一个矩阵的列数必须与第二个矩阵中的行数相同。 例如，4 × 2 矩阵以生成的 4 × 3 矩阵 2 × 3 矩阵相乘。  
  
 可以将平面行和列的矩阵中的点视为向量。 例如，（2，5） 是包含两个组件，矢量和 （3，7，1） 是一个具有三个组件的向量。 定义两个向量的点积，如下所示：  
  
 (a，b） • (c、 d) = ac + bd  
  
 (a、 b、 c） • （d、 e、 f） = ad + 是 + cf  
  
 例如的点积 （2，3） 和 （5，4） 是 (2)(5) + (3)(4) = 22。 （2，5，1） 的点积和 （4，3，1） 是 (2)(4) + (5)(3) + (1)(1) = 24。 请注意，两个向量的点积数字，而不是另一个矢量。 另请注意，仅当两个向量具有相同数目的组件，可以计算点积。  
  
 让 A(i, j) 是第 i 个行和 jth 列中的一个矩阵中的条目。 例如 A （3，2） 是第三行和第二列中的一个矩阵中的输入。 假设 A、 B 和 C 是矩阵和 AB = c。C 的条目进行计算，如下所示：  
  
 C （i，j） = （A 的第 i 行） • （B 的列 j）  
  
 下图显示了几个示例的矩阵乘法。  
  
 ![Transformations](./media/aboutgdip05-art06.gif "AboutGdip05_art06")  
  
 如果您认为的 1 × 2 矩阵作为平面中的点，你可以通过将其乘以 2 × 2 矩阵转换该点。 下图显示了多个转换应用于点 （2，1）。  
  
 ![Transformations](./media/aboutgdip05-art07.gif "AboutGdip05_art07")  
  
 所有在上图中所示的转换都是线性转换。 某些其他转换，如转换时，不是线性的并且不能表示为 2 × 2 矩阵相乘。 假设你想开始使用点 （2，1），将其旋转 90 度，将其转换在 x 方向的 3 个单位并将其沿 y 方向的 4 个单位。 可以使用矩阵乘法和矩阵添加来完成此操作。  
  
 ![Transformations](./media/aboutgdip05-art08.gif "AboutGdip05_art08")  
  
 线性转换 （2 × 2 矩阵相乘） 后, 跟的翻译 （1 × 2 矩阵的加法） 称为仿射转换。 存储仿射转换矩阵 （一个用于线性部分），一个用于转换的一对中的替代方法是在 3 × 3 矩阵中存储整个转换。 若要实现此目的，平面中的点必须存储在具有虚拟的第三个坐标的 1 × 3 矩阵。 通常的方法是使所有第三个坐标等于 1。 例如，由矩阵 [2 1 1] 表示点 （2，1）。 下图显示了仿射转换 （旋转 90 度; 转换在 x 方向的 3 个单位，在 y 方向的 4 个单位） 表示为单个 3 × 3 矩阵相乘。  
  
 ![Transformations](./media/aboutgdip05-art09.gif "AboutGdip05_art09")  
  
 在上述示例中，（2，1） 的点到点 （2，6） 映射。 请注意，3 × 3 矩阵的第三个列包含数字 0，0，1。 此属性始终为仿射转换 3 × 3 矩阵的大小写。 重要的数字是 1 和 2 列中的六个数字。 矩阵的左上方 2 × 2 部分表示的线性转换，一部分和第三行中的前两个条目表示平移。  
  
 ![Transformations](./media/aboutgdip05-art10.gif "AboutGdip05_art10")  
  
 在中[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)]可以存储在一个仿射转换<xref:System.Drawing.Drawing2D.Matrix>对象。 因为表示仿射转换矩阵的第三个列始终为 （0，0，1） 中的前两个列中指定仅六个数字，在构造时<xref:System.Drawing.Drawing2D.Matrix>对象。 该语句`Matrix myMatrix = new Matrix(0, 1, -1, 0, 3, 4)`构造在上图中所示的矩阵。  
  
## <a name="composite-transformations"></a>复合转换  
 复合转换是一系列转换后, 跟另一个。 请考虑矩阵和在下面的列表中的转换：  
  
|||  
|-|-|  
|矩阵 A|旋转 90 度|  
|矩阵 B|通过沿 x 方向的 2 倍缩放|  
|矩阵 C|转换在 y 方向的 3 个单位|  
  
 如果我们使用点 （2，1）-由矩阵 [2 1 1] 表示 — 乘以 A、 B、，然后 C，（2，1） 的点将进行按所列顺序的三个转换。  
  
 [2 1 1]ABC = [-2 5 1]  
  
 而是不是存储在三个单独的矩阵复合转换的三个部分，您可以乘以 A、 B 和 C 一起以获取存储整个复合转换的一个 3 × 3 矩阵。 假设 ABC = d。然后，乘以 D 的点提供相同的结果为点乘以 A、 B，然后按 c。  
  
 [2 1 1]D = [-2 5 1]  
  
 下图显示了矩阵 A、 B、 C 和 d。  
  
 ![Transformations](./media/aboutgdip05-art12.gif "AboutGdip05_art12")  
  
 复合转换的矩阵，可以通过将单独的变换矩阵相乘格式正确的事实意味着仿射转换任何序列可以存储在单个<xref:System.Drawing.Drawing2D.Matrix>对象。  
  
> [!CAUTION]
>  复合转换的顺序非常重要。 一般情况下，旋转，然后扩展，然后转换是不相同的小数位数为然后旋转，然后转换。 同样，矩阵乘法的顺序非常重要。 一般情况下，ABC 不与备份相同。  
  
 <xref:System.Drawing.Drawing2D.Matrix>类提供用于构建复合转换的多种方法： <xref:System.Drawing.Drawing2D.Matrix.Multiply%2A>， <xref:System.Drawing.Drawing2D.Matrix.Rotate%2A>， <xref:System.Drawing.Drawing2D.Matrix.RotateAt%2A>， <xref:System.Drawing.Drawing2D.Matrix.Scale%2A>， <xref:System.Drawing.Drawing2D.Matrix.Shear%2A>，和<xref:System.Drawing.Drawing2D.Matrix.Translate%2A>。 下面的示例创建一个复合转换，它先旋转 30 度，然后按 2 在 y 方向中的因子缩放，然后会在 x 方向的 5 个单位将转换的矩阵。  
  
 [!code-csharp[System.Drawing.CoordinateSystems#11](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.CoordinateSystems#11](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/VB/Class1.vb#11)]  
  
 下图显示了矩阵。  
  
 ![Transformations](./media/aboutgdip05-art13.gif "AboutGdip05_art13")  
  
## <a name="see-also"></a>请参阅
- [坐标系统和转换](coordinate-systems-and-transformations.md)
- [在托管 GDI+ 中使用转换](using-transformations-in-managed-gdi.md)
