---
title: 如何：Windows 窗体 ListView 控件中选择一项
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- lists [Windows Forms], selecting items
- ListView control [Windows Forms], selecting items
- selection [Windows Forms], in list views
- list views [Windows Forms], selecting items
ms.assetid: ddea918e-1ddf-47f4-bd09-1e9b4c9d0c39
ms.openlocfilehash: 09ec0b60e5d591f4cc66cf5ed454576203afa473
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57707023"
---
# <a name="how-to-select-an-item-in-the-windows-forms-listview-control"></a>如何：Windows 窗体 ListView 控件中选择一项
此示例演示如何以编程方式在 Windows 窗体中选择一项<xref:System.Windows.Forms.ListView>控件。 以编程方式选择某个项不会自动更改焦点<xref:System.Windows.Forms.ListView>控件。 出于此原因，你通常还需要设置的项，因为聚焦时选择某一项。  
  
## <a name="example"></a>示例  
 [!code-csharp[System.Windows.Forms.ListView.Misc#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListView.Misc/CS/form1.cs#1)]
 [!code-vb[System.Windows.Forms.ListView.Misc#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListView.Misc/VB/form1.vb#1)]  
  
## <a name="compiling-the-code"></a>编译代码  
 此示例需要：  
  
-   一个<xref:System.Windows.Forms.ListView>名为控件`listView1`，其中包含至少一个项。  
  
-   对 <xref:System?displayProperty=nameWithType> 和 <xref:System.Windows.Forms?displayProperty=nameWithType> 命名空间的引用。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.ListView>
- <xref:System.Windows.Forms.ListViewItem.Selected%2A?displayProperty=nameWithType>
