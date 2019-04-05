---
title: 如何：指定自定义 Popup 位置
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Popup control [WPF], specifying custom position
ms.assetid: 28c24f39-d3aa-4ee2-b950-384b4a5dab92
ms.openlocfilehash: 2ffba3d1a0fee236f803dd5877d541084192418b
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57358478"
---
# <a name="how-to-specify-a-custom-popup-position"></a>如何：指定自定义 Popup 位置
此示例演示如何指定的自定义位置<xref:System.Windows.Controls.Primitives.Popup>控制何时<xref:System.Windows.Controls.Primitives.Popup.Placement%2A>属性设置为<xref:System.Windows.Controls.Primitives.PlacementMode.Custom>。  
  
## <a name="example"></a>示例  
 当<xref:System.Windows.Controls.Primitives.Popup.Placement%2A>属性设置为<xref:System.Windows.Controls.Primitives.PlacementMode.Custom>，则<xref:System.Windows.Controls.Primitives.Popup>调用的定义的实例<xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback>委托。 此委托返回的可能是相对于目标区域的左上的角和的左上的角的点集<xref:System.Windows.Controls.Primitives.Popup>。 <xref:System.Windows.Controls.Primitives.Popup>位置出现在提供最佳的可见性的点。  
  
 下面的示例演示如何定义的位置<xref:System.Windows.Controls.Primitives.Popup>通过设置<xref:System.Windows.Controls.Primitives.Popup.Placement%2A>属性设置为<xref:System.Windows.Controls.Primitives.PlacementMode.Custom>。 它还演示如何创建和分配<xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback>委托以定位<xref:System.Windows.Controls.Primitives.Popup>。  回调委托返回两个<xref:System.Windows.Controls.Primitives.CustomPopupPlacement>对象。  如果<xref:System.Windows.Controls.Primitives.Popup>情况下的第一个位置，在屏幕边缘隐藏<xref:System.Windows.Controls.Primitives.Popup>放在第二个位置。  
  
 [!code-xaml[PopupCustomPlacement#CustomPlacement](~/samples/snippets/csharp/VS_Snippets_Wpf/PopupCustomPlacement/CSharp/Window1.xaml#customplacement)]  
  
 [!code-csharp[PopupCustomPlacement#DelegateInstance](~/samples/snippets/csharp/VS_Snippets_Wpf/PopupCustomPlacement/CSharp/Window1.xaml.cs#delegateinstance)]
 [!code-vb[PopupCustomPlacement#DelegateInstance](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PopupCustomPlacement/visualbasic/window1.xaml.vb#delegateinstance)]  
  
 [!code-csharp[PopupCustomPlacement#DelegateDefinition](~/samples/snippets/csharp/VS_Snippets_Wpf/PopupCustomPlacement/CSharp/Window1.xaml.cs#delegatedefinition)]
 [!code-vb[PopupCustomPlacement#DelegateDefinition](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PopupCustomPlacement/visualbasic/window1.xaml.vb#delegatedefinition)]  
  
 有关完整示例，请参阅[Popup 放置示例](https://go.microsoft.com/fwlink/?LinkID=160032)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Controls.Primitives.Popup>
- [Popup 概述](popup-overview.md)
- [帮助主题](popup-how-to-topics.md)
