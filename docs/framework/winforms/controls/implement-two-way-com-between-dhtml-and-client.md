---
title: 如何：DHTML 代码和客户端应用程序代码之间实现双向通信
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
f1_keywords:
- WebBrowser.ObjectForScripting
- WebBrowser.Document
helpviewer_keywords:
- WebBrowser control [Windows Forms], examples
- communications [Windows Forms], DHTML and client applications
- examples [Windows Forms], WebBrowser control
- WebBrowser control [Windows Forms], communication between DHTML and client application
- DHTML [Windows Forms], embedding in Windows Forms
ms.assetid: 55353a32-b09e-4479-a521-ff3a5ff9a708
ms.openlocfilehash: 52928b11ce3577a1fb6d218b4a74b986f5fe8d1e
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57710259"
---
# <a name="how-to-implement-two-way-communication-between-dhtml-code-and-client-application-code"></a>如何：DHTML 代码和客户端应用程序代码之间实现双向通信
可使用 <xref:System.Windows.Forms.WebBrowser> 控件将现有的动态 HTML (DHTML) Web 应用程序代码添加到 Windows 窗体客户端应用程序。 如果已投入大量的开发时间用于创建基于 DHTML 的控件，并且想要利用 Windows 窗体丰富的用户界面功能，而无需重写现有代码，这将非常有用。  
  
 <xref:System.Windows.Forms.WebBrowser> 控件使你通过 <xref:System.Windows.Forms.WebBrowser.ObjectForScripting%2A> 和 <xref:System.Windows.Forms.WebBrowser.Document%2A> 属性可以实现客户端应用程序代码和 Web 页的脚本代码间的双向通信。 此外，还可以配置 <xref:System.Windows.Forms.WebBrowser> 控件，以便 Web 控件与应用程序窗体上的其他控件的无缝混合，从而隐藏其 DHTML 实现。 若要无缝地混合控件，需格式化显示的页面，使其背景色和视觉样式可匹配窗体中的其余部分，并使用 <xref:System.Windows.Forms.WebBrowser.AllowWebBrowserDrop%2A>、<xref:System.Windows.Forms.WebBrowser.IsWebBrowserContextMenuEnabled%2A>和 <xref:System.Windows.Forms.WebBrowser.WebBrowserShortcutsEnabled%2A> 属性禁用标准的浏览器功能。  
  
### <a name="to-embed-dhtml-in-your-windows-forms-application"></a>若要在 Windows 窗体应用程序中嵌入 DHTML  
  
1.  需将 <xref:System.Windows.Forms.WebBrowser> 控件的 <xref:System.Windows.Forms.WebBrowser.AllowWebBrowserDrop%2A> 属性设置为 `false`，以防止 <xref:System.Windows.Forms.WebBrowser> 控件打开放到其上的文件。  
  
     [!code-csharp[System.Windows.Forms.WebBrowser.ObjectForScripting#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/CS/form1.cs#1)]
     [!code-vb[System.Windows.Forms.WebBrowser.ObjectForScripting#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/vb/form1.vb#1)]  
  
2.  将控件的 <xref:System.Windows.Forms.WebBrowser.IsWebBrowserContextMenuEnabled%2A> 属性设置为 `false`，以防止 <xref:System.Windows.Forms.WebBrowser> 控件在用户进行右键单击时，显示其快捷方式菜单。  
  
     [!code-csharp[System.Windows.Forms.WebBrowser.ObjectForScripting#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/CS/form1.cs#2)]
     [!code-vb[System.Windows.Forms.WebBrowser.ObjectForScripting#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/vb/form1.vb#2)]  
  
3.  将控件的 <xref:System.Windows.Forms.WebBrowser.WebBrowserShortcutsEnabled%2A> 属性设置为 `false`，以防止 <xref:System.Windows.Forms.WebBrowser> 控件响应快捷键。  
  
     [!code-csharp[System.Windows.Forms.WebBrowser.ObjectForScripting#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/CS/form1.cs#3)]
     [!code-vb[System.Windows.Forms.WebBrowser.ObjectForScripting#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/vb/form1.vb#3)]  
  
4.  在窗体的构造函数或 <xref:System.Windows.Forms.Form.Load> 事件处理程序中设置 <xref:System.Windows.Forms.WebBrowser.ObjectForScripting%2A> 属性。  
  
     以下代码将窗体类自身用于脚本对象。  
  
    > [!NOTE]
    >  组件对象模型 (COM) 必须能够访问脚本对象。 若要使窗体对 COM 可见，则将 <xref:System.Runtime.InteropServices.ComVisibleAttribute> 属性添加到窗体类中。  
  
     [!code-csharp[System.Windows.Forms.WebBrowser.ObjectForScripting#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/CS/form1.cs#4)]
     [!code-vb[System.Windows.Forms.WebBrowser.ObjectForScripting#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/vb/form1.vb#4)]  
  
5.  实现脚本代码将使用的应用程序代码中的公共属性或方法。  
  
     例如，如果对脚本对象使用窗体类，则将以下代码添加到窗体类中。  
  
     [!code-csharp[System.Windows.Forms.WebBrowser.ObjectForScripting#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/CS/form1.cs#5)]
     [!code-vb[System.Windows.Forms.WebBrowser.ObjectForScripting#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/vb/form1.vb#5)]  
  
6.  在脚本代码中使用 `window.external` 对象来访问指定对象的公共属性和方法。  
  
     以下 HTML 代码演示如何通过单击按钮对脚本对象调用方法。 将此代码复制到 HTML 文档的 BODY 元素中，该文档为使用控件的 <xref:System.Windows.Forms.WebBrowser.Navigate%2A> 方法所加载的文档，或将其分配到控件的 <xref:System.Windows.Forms.WebBrowser.DocumentText%2A> 属性的文档。  
  
    ```  
    <button onclick="window.external.Test('called from script code')">  
        call client code from script code  
    </button>  
    ```  
  
7.  实现应用程序代码将使用的脚本代码中的函数。  
  
     以下 HTML SCRIPT 元素提供了示例函数。 将此代码复制到 HTML 文档的 HEAD 元素中，该文档为使用控件的 <xref:System.Windows.Forms.WebBrowser.Navigate%2A> 方法所加载的文档，或将其分配到控件的 <xref:System.Windows.Forms.WebBrowser.DocumentText%2A> 属性的文档。  
  
    ```  
    <script>  
    function test(message) {   
        alert(message);   
    }  
    </script>  
    ```  
  
8.  使用 <xref:System.Windows.Forms.WebBrowser.Document%2A> 属性访问客户端应用程序代码中的脚本代码。  
  
     例如，将以下代码添加到按钮 <xref:System.Windows.Forms.Control.Click> 事件处理程序中。  
  
     [!code-csharp[System.Windows.Forms.WebBrowser.ObjectForScripting#8](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/CS/form1.cs#8)]
     [!code-vb[System.Windows.Forms.WebBrowser.ObjectForScripting#8](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/vb/form1.vb#8)]  
  
9. 完成 DHTML 调试后，将控件的 <xref:System.Windows.Forms.WebBrowser.ScriptErrorsSuppressed%2A> 属性设置为 `true`，以防止 <xref:System.Windows.Forms.WebBrowser> 控件显示脚本代码问题的错误消息。  
  
     [!code-csharp[System.Windows.Forms.WebBrowser.ObjectForScripting#9](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/CS/form1.cs#9)]
     [!code-vb[System.Windows.Forms.WebBrowser.ObjectForScripting#9](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/vb/form1.vb#9)]  
  
## <a name="example"></a>示例  
 以下完整的代码示例将提供演示应用程序，以方便用于理解此功能。 HTML 代码将通过 <xref:System.Windows.Forms.WebBrowser.DocumentText%2A> 属性加载到 <xref:System.Windows.Forms.WebBrowser> 控件中，而不是从单独的 HTML 文件进行加载。  
  
 [!code-csharp[System.Windows.Forms.WebBrowser.ObjectForScripting#0](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/CS/form1.cs#0)]
 [!code-vb[System.Windows.Forms.WebBrowser.ObjectForScripting#0](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/vb/form1.vb#0)]  
  
## <a name="compiling-the-code"></a>编译代码  
 此代码需要：  
  
-   对 System 和 System.Windows.Forms 程序集的引用。  
  
 Visual Basic 或 Visual C# 生成命令行中的此示例的信息，请参阅[从命令行生成](../../../visual-basic/reference/command-line-compiler/building-from-the-command-line.md)或[命令行上使用 csc.exe](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)。 也可以通过将代码粘贴到新的项目中生成此示例在 Visual Studio 中。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.WebBrowser>
- <xref:System.Windows.Forms.WebBrowser.Document%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.WebBrowser.ObjectForScripting%2A?displayProperty=nameWithType>
- [WebBrowser 控件](webbrowser-control-windows-forms.md)
