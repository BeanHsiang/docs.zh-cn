---
title: 如何：测试 Point4D 结构是否相等和不相等
ms.date: 03/30/2017
helpviewer_keywords:
- inequality [WPF], testing Point4D structures for
- equality [WPF], testing Point4D structures for
- testing [WPF], Point4D structures for equality
- Point4D structures [WPF], testing for inequality
- testing [WPF], Point4D structures for inequality
- Point4D structures [WPF], testing for equality
ms.assetid: e004a67e-db7f-4af8-a31f-e6b2a44ccf34
ms.openlocfilehash: d72aef8a1328742f0b04c2ad009126e21390398a
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57367201"
---
# <a name="how-to-test-point4d-structures-for-equality-and-inequality"></a>如何：测试 Point4D 结构是否相等和不相等
此示例显示了如何测试<xref:System.Windows.Media.Media3D.Point4D>结构是否相等和不相等。  
  
 下面的代码演示如何测试<xref:System.Windows.Media.Media3D.Point4D>结构是否相等和不相等使用<xref:System.Windows.Media.Media3D.Point4D>相等性的方法。  <xref:System.Windows.Media.Media3D.Point4D>结构测试相等性使用重载的等式 (`==`) 运算符，然后使用重载的不相等的不相等 (`!=`) 运算符，并最后<xref:System.Windows.Media.Media3D.Point3D>结构和一个<xref:System.Windows.Media.Media3D.Point4D>使用静态相等性检查结构<xref:System.Windows.Media.Media3D.Point4D.Equals%2A>方法。  
  
## <a name="example"></a>示例  
 [!code-csharp[3DGallery_procedural_snip#Point4DEqualityExample_csharp](~/samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_procedural_snip/CSharp/Misc3DOperationsExample.cs#point4dequalityexample_csharp)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Media.Media3D.Point4D.op_Equality%2A>
- <xref:System.Windows.Media.Media3D.Point4D.op_Inequality%2A>
- <xref:System.Windows.Media.Media3D.Point4D.Equals%2A>
