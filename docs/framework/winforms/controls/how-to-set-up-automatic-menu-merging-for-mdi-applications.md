---
title: 如何：设置自动菜单合并为 MDI 应用程序
ms.date: 03/30/2017
helpviewer_keywords:
- MenuStrip [Windows Forms], merging
- Merging [Windows Forms], automatic menu
ms.assetid: 55e32cad-1141-4a56-aa33-d9543ca3d393
ms.openlocfilehash: 152db39e7c947d5a49eaed81b00d13c02aa8014c
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57719723"
---
# <a name="how-to-set-up-automatic-menu-merging-for-mdi-applications"></a>如何：设置自动菜单合并为 MDI 应用程序
以下过程提供的基本步骤用于设置在多文档界面 (MDI) 应用程序中使用自动合并<xref:System.Windows.Forms.MenuStrip>。  
  
### <a name="to-set-up-automatic-menu-merging"></a>若要设置自动菜单合并  
  
1.  创建 MDI 父窗体通过设置其<xref:System.Windows.Forms.Form.IsMdiContainer%2A>属性设置为`true`。  
  
2.  添加<xref:System.Windows.Forms.MenuStrip>到 MDI 父，设置其<xref:System.Windows.Forms.Form.MainMenuStrip%2A>属性设置为的<xref:System.Windows.Forms.MenuStrip>。  
  
3.  创建 MDI 子窗体，并设置其<xref:System.Windows.Forms.Form.MdiParent%2A>属性设置为父窗体的名称。  
  
4.  添加<xref:System.Windows.Forms.MenuStrip>到 MDI 子窗体。  
  
5.  在子窗体上设置<xref:System.Windows.Forms.ToolStripItem.Visible%2A>的属性<xref:System.Windows.Forms.MenuStrip>到`false`。  
  
6.  将菜单项添加到子窗体<xref:System.Windows.Forms.MenuStrip>你想要合并到父窗体的<xref:System.Windows.Forms.MenuStrip>时激活子窗体。  
  
7.  使用<xref:System.Windows.Forms.ToolStripItem.MergeAction%2A>菜单上的属性项中的子窗体<xref:System.Windows.Forms.MenuStrip>来控制如何将它们合并到父窗体。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.MenuStrip>
- <xref:System.Windows.Forms.ToolStripMenuItem>
- [MenuStrip 控件概述](menustrip-control-overview-windows-forms.md)
