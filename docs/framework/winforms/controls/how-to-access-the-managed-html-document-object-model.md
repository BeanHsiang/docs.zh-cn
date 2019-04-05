---
title: 如何：访问托管的 HTML 文档对象模型
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- HTML DOM [Windows Forms], accessing
- managed HTML DOM [Windows Forms], accessing
ms.assetid: 40fa5cd5-1ed8-42f6-a93f-9ac01608bbeb
ms.openlocfilehash: f2e2593b161a0dc072f0ecaa872bfa9ab83ac24c
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57715940"
---
# <a name="how-to-access-the-managed-html-document-object-model"></a>如何：访问托管的 HTML 文档对象模型
可以从两种类型的应用程序访问托管 HTML 文档对象模型 (DOM)：  
  
-   承载了托管 <xref:System.Windows.Forms.WebBrowser> 控件的 Windows 窗体应用程序 (.exe)。 这两种技术互相补充，<xref:System.Windows.Forms.WebBrowser> 控件向用户显示页面，HTML DOM 表示文档的逻辑结构。  
  
-   在 Internet Explorer 内托管的 Windows 窗体 <xref:System.Windows.Forms.UserControl>。 你可以访问表示托管你的 <xref:System.Windows.Forms.UserControl> 的页面的 HTML DOM，以更改文档结构或打开模式对话框（还有很多其他可能的操作）。  
  
### <a name="to-access-dom-from-a-windows-forms-application"></a>从 Windows 窗体应用程序访问 DOM  
  
1.  在 Windows 窗体应用程序内部托管 <xref:System.Windows.Forms.WebBrowser> 控件，并监视 <xref:System.Windows.Forms.WebBrowser.DocumentCompleted> 事件。 有关托管控件和监视事件的详细信息，请参阅[事件](../../../standard/events/index.md)。  
  
2.  通过访问 <xref:System.Windows.Forms.HtmlDocument> 控件的 <xref:System.Windows.Forms.WebBrowser.Document%2A> 属性，从 <xref:System.Windows.Forms.WebBrowser> 中检索当前页。  

### <a name="to-access-dom-from-a-usercontrol-hosted-in-internet-explorer"></a>从在 Internet Explorer 中托管的 UserControl 访问 DOM  
  
1.  从 <xref:System.Windows.Forms.UserControl> 类创建你自己的自定义派生类。 有关详细信息，请参阅[如何：创作复合控件](how-to-author-composite-controls.md)。  
  
2.  将以下代码放置在你的 <xref:System.Windows.Forms.UserControl> 的 Load 事件处理程序中：  
  
 [!code-csharp[AccessHTMLDOMControl#1](~/samples/snippets/csharp/VS_Snippets_Winforms/AccessHTMLDOMControl/cs/UserControl1.cs#1)]
 [!code-vb[AccessHTMLDOMControl#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/AccessHTMLDOMControl/vb/UserControl1.vb#1)]  
  
## <a name="robust-programming"></a>可靠编程  
  
1.  通过 <xref:System.Windows.Forms.WebBrowser> 控件使用 DOM 时，总是应等到 <xref:System.Windows.Forms.WebBrowser.DocumentCompleted> 事件发生之后，再尝试访问 <xref:System.Windows.Forms.WebBrowser.Document%2A> 控件的 <xref:System.Windows.Forms.WebBrowser> 属性。 加载整个文档之后会引发 <xref:System.Windows.Forms.WebBrowser.DocumentCompleted> 事件；如果你在此之前用过 DOM，则有导致应用程序中出现运行时异常的风险。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
  
1.  你的应用程序或 <xref:System.Windows.Forms.UserControl> 将需要完全信任，才能访问托管 HTML DOM。 如果使用 [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)] 部署 Windows 窗体应用程序，则可使用“权限提升”或“受信任的应用程序部署”来请求完全信任；有关详细信息，请参阅[保护 ClickOnce 应用程序](/visualstudio/deployment/securing-clickonce-applications)。  
  
## <a name="see-also"></a>请参阅
- [使用托管 HTML 文档对象模型](using-the-managed-html-document-object-model.md)
