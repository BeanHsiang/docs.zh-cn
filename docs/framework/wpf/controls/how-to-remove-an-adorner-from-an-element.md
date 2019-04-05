---
title: 如何：从元素移除装饰器
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- adorners [WPF], removing
ms.assetid: 97cf4d9f-0596-429e-8526-32a30aa4ae99
ms.openlocfilehash: 0c74fe9ed1e7190ce4ff26a7dbae1413f950ba7e
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57374071"
---
# <a name="how-to-remove-an-adorner-from-an-element"></a>如何：从元素移除装饰器
此示例演示如何以编程方式删除特定的装饰器从指定<xref:System.Windows.UIElement>。  
  
## <a name="example"></a>示例  
 此详细的代码示例的装饰器返回的数组中移除第一个装饰器<xref:System.Windows.Documents.AdornerLayer.GetAdorners%2A>。  此示例检索在装饰器恰好<xref:System.Windows.UIElement>名为*myTextBox*。  如果在调用中指定元素<xref:System.Windows.Documents.AdornerLayer.GetAdorners%2A>有任何装饰器，`null`返回。  此代码显式检查 null 的数组，并最适合应用程序的空数组的地方是比较常见。  
  
 [!code-csharp[AdornersMiscCode#_RemoveSpecificAdornerLong](~/samples/snippets/csharp/VS_Snippets_Wpf/AdornersMiscCode/CSharp/Window1.xaml.cs#_removespecificadornerlong)]
 [!code-vb[AdornersMiscCode#_RemoveSpecificAdornerLong](~/samples/snippets/visualbasic/VS_Snippets_Wpf/AdornersMiscCode/visualbasic/window1.xaml.vb#_removespecificadornerlong)]  
  
## <a name="example"></a>示例  
 此简化的代码示例是功能上等效于上面所示的详细示例。 此代码不显式检查 null 数组，因此很可能，<xref:System.NullReferenceException>可能引发异常。  Null 数组的地方很少出现，此代码是最适合应用程序。  
  
 [!code-csharp[AdornersMiscCode#_RemoveSpecificAdornerShort](~/samples/snippets/csharp/VS_Snippets_Wpf/AdornersMiscCode/CSharp/Window1.xaml.cs#_removespecificadornershort)]
 [!code-vb[AdornersMiscCode#_RemoveSpecificAdornerShort](~/samples/snippets/visualbasic/VS_Snippets_Wpf/AdornersMiscCode/visualbasic/window1.xaml.vb#_removespecificadornershort)]  
  
## <a name="see-also"></a>请参阅
- [装饰器概述](adorners-overview.md)
