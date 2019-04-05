---
title: 在托管 HTML 文档对象模型中访问框架
ms.date: 03/30/2017
helpviewer_keywords:
- HTML [Windows Forms], dOM
- managed HTML DOM
- HTML [Windows Forms], managed
- HTML DOM [Windows Forms], managed
- frames [Windows Forms], accessing
- DOM [Windows Forms], accessing frames in managed HTML
ms.assetid: cdeeaa22-0be4-4bbf-9a75-4ddc79199f8d
ms.openlocfilehash: f02e5cf054f8891b134ee914b54e22e975d835a9
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57723785"
---
# <a name="accessing-frames-in-the-managed-html-document-object-model"></a>在托管 HTML 文档对象模型中访问框架
一些 HTML 文档组成共*帧*，或可以存放其自己独特的 HTML 文档的 windows。 使用框架可以轻松地创建 HTML 页面，页面中的一个或多个部分（如导航栏）保持静态，而其它框架则不断更改内容。  
  
 HTML 作者可通过以下两种方式之一创建框架：  
  
-   使用 `FRAMESET` 和 `FRAME` 标记，创建固定窗口。  
  
 - 或 -  
  
-   使用 `IFRAME` 标记，创建一个可以在运行时重新定位的浮动窗口。  
  
1.  由于框架包含 HTML 文档，所以它们在文档对象模型 (DOM) 中表示为窗口元素和框架元素。  
  
2.  通过使用 <xref:System.Windows.Forms.HtmlWindow> 的框架集合访问 `FRAME` 或 `IFRAME` 标记时，就是在检索与该框架对应的窗口元素。 这表示框架的所有动态属性，如框架的当前 URL、文档和大小。  
  
3.  通过使用 <xref:System.Windows.Forms.HtmlWindow> 的 <xref:System.Windows.Forms.HtmlWindow.WindowFrameElement%2A> 属性、<xref:System.Windows.Forms.HtmlElement.Children%2A> 集合或者诸如 <xref:System.Windows.Forms.HtmlElementCollection.GetElementsByName%2A> 或 <xref:System.Windows.Forms.HtmlDocument.GetElementById%2A> 等方法访问 `FRAME` 或 `IFRAME` 标记时，就是在检索框架元素。 这表示框架的静态属性，包括原始 HTML 文件中指定的 URL。  
  
## <a name="frames-and-security"></a>框架和安全性  
 对框架的访问复杂，因为托管的 HTML DOM 实现称为一种安全措施*跨框架脚本安全*。 如果文档包含在不同域中具有两个或多个 `FRAME` 的 `FRAMESET`，则这些 `FRAME` 相互之间不能交互。 换而言之，`FRAME`网站上的显示内容不能访问中的信息`FRAME`如承载第三方站点的`http://www.adatum.com/`。 在 <xref:System.Windows.Forms.HtmlWindow> 类级别实现此安全。 可以获取有关托管另一个网站的 `FRAME` 的常规信息（如其 URL），但不能访问其 <xref:System.Windows.Forms.HtmlWindow.Document%2A> 或更改其宿主 `FRAME` 或 `IFRAME` 的大小或位置。  
  
 此规则也适用于使用 <xref:System.Windows.Forms.HtmlWindow.Open%2A> 和 <xref:System.Windows.Forms.HtmlWindow.OpenNew%2A> 方法打开的窗口。 如果打开的窗口位于与 <xref:System.Windows.Forms.WebBrowser> 控件中托管的页面不同的域中，则你将不能移动该窗口或检查其内容。 如果使用 <xref:System.Windows.Forms.WebBrowser> 控件来显示与用于部署基于 Windows 窗体的应用程序的网站不同的网站，也会强制这些限制。 如果使用 [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)] 部署技术来安装来自网站 A 的应用程序，并且使用 <xref:System.Windows.Forms.WebBrowser> 来显示网站 B，将不能访问网站 B 的数据。  
  
## <a name="see-also"></a>请参阅
- [\<帧 > 元素](https://developer.mozilla.org/docs/Web/HTML/Element/frame)
- [使用托管 HTML 文档对象模型](using-the-managed-html-document-object-model.md)
