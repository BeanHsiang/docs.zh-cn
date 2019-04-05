---
title: TableLayoutPanel 控件的最佳做法
ms.date: 03/30/2017
helpviewer_keywords:
- layout [Windows Forms]
- TableLayoutPanel control [Windows Forms], best practices
- forms [Windows Forms], best practices
- AutoSize property [Windows Forms], tableLayoutPanel control
- controls [Windows Forms], sizing
- TableLayoutPanel control [Windows Forms], AutoSize behavior
- layout [Windows Forms], AutoSize
- layout [Windows Forms], best practices
- best practices [Windows Forms], tableLayoutPanel control
- sizing [Windows Forms], automatic
- automatic sizing
ms.assetid: b6706efb-d7a4-45ec-8cf4-08fa993e3afb
ms.openlocfilehash: 6be6d0904d5b52e5188f0a5a16aaefa08265379c
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54674188"
---
# <a name="best-practices-for-the-tablelayoutpanel-control"></a>TableLayoutPanel 控件的最佳做法
<xref:System.Windows.Forms.TableLayoutPanel>控件提供了强大的布局功能，应在 Windows 窗体上使用之前仔细考虑。  
  
## <a name="recommendations"></a>建议  
 以下建议将帮助你使用<xref:System.Windows.Forms.TableLayoutPanel>最有效地控制。  
  
### <a name="targeted-use"></a>目标的使用  
 使用<xref:System.Windows.Forms.TableLayoutPanel>谨慎控制。 不应使用它在所有情况下，需要可调整大小的布局。 以下列表介绍从使用获益最多的布局<xref:System.Windows.Forms.TableLayoutPanel>控件：  
  
-   其中有个彼此的按比例调整大小的多个部分的窗体的布局。  
  
-   将修改或在运行时，如数据输入窗体具有加上或减去的用户可自定义字段的动态生成的布局根据首选项。  
  
-   应保持为整体的固定大小的布局。 例如，可能有一个对话框，应保持小于 800 x 600，但你需要支持本地化的字符串。  
  
 以下列表介绍执行不会大大受益于使用的布局<xref:System.Windows.Forms.TableLayoutPanel>控件：  
  
-   简单数据输入窗体包含单个列的标签和文本输入区域的单个列。  
  
-   含有单个较大的窗体显示在调整大小时应填充所有可用空间的区域。 此示例是窗体中显示单个<xref:System.Windows.Forms.PropertyGrid>控件。 在这种情况下，使用定位功能，因为没有其他应展开时调整窗体。  
  
 请仔细选择哪些控件必须位于<xref:System.Windows.Forms.TableLayoutPanel>控件。 如果为文本使用锚定的 30%的增长留出空间，请考虑使用<xref:System.Windows.Forms.Control.Anchor%2A>只属性。 如果在可以估计您的布局所需的空间，请使用<xref:System.Windows.Forms.Control.Dock%2A>并<xref:System.Windows.Forms.Control.Anchor%2A>是更容易估计的剩余空间的详细信息和<xref:System.Windows.Forms.Control.AutoSize%2A>行为。  
  
 通常，当设计与布局中<xref:System.Windows.Forms.TableLayoutPanel>控件，使设计尽可能简单。  
  
### <a name="use-the-document-outline-window"></a>使用文档大纲窗口  
 文档大纲窗口提供了您的布局，可用于处理您的控件的 z 顺序和父-子关系的树视图。 从**视图菜单**，选择**其他 Windows**，然后选择**文档大纲**。  
  
### <a name="avoid-nesting"></a>避免嵌套  
 避免其他嵌套<xref:System.Windows.Forms.TableLayoutPanel>控件的<xref:System.Windows.Forms.TableLayoutPanel>控件。 调试嵌套的布局可能很困难。  
  
### <a name="avoid-visual-inheritance"></a>避免 Visual 继承  
 <xref:System.Windows.Forms.TableLayoutPanel>控件在 Windows 窗体设计器中不支持 visual 继承。 一个<xref:System.Windows.Forms.TableLayoutPanel>派生类中的控件将显示为"已锁定"在设计时。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.TableLayoutPanel>
- <xref:System.Windows.Forms.FlowLayoutPanel>
