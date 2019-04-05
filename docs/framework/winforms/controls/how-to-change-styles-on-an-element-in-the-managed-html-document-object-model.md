---
title: 如何：更改在托管的 HTML 文档对象模型中元素的样式
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- managed HTML DOM [Windows Forms], changing styles on elements
ms.assetid: 154e8d9f-3e2d-4e8b-a6f3-c85a070e9cc1
ms.openlocfilehash: a1abfaeab735746edbf089d576dc6f56dc4a6eea
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57712768"
---
# <a name="how-to-change-styles-on-an-element-in-the-managed-html-document-object-model"></a>如何：更改在托管的 HTML 文档对象模型中元素的样式

可以使用以 html 格式的样式来控制文档和其元素的外观。 <xref:System.Windows.Forms.HtmlDocument> 并<xref:System.Windows.Forms.HtmlElement>支持<xref:System.Windows.Forms.HtmlElement.Style%2A>采用以下格式的样式字符串属性：

`name1:value1;...;nameN:valueN;`

下面是`DIV`设置为 Arial，所有文本为粗体的字体的样式字符串：

`<DIV style="font-face:arial;font-weight:bold;">`

`Hello, world!`

`</DIV>`

操作使用的样式问题<xref:System.Windows.Forms.HtmlElement.Style%2A>属性是可以证明难以将添加到和从字符串中删除单独的样式设置。 例如，它将变得很复杂的过程，以便呈现斜体中前面的文本，只要用户将光标放置`DIV`，并当光标离开去掉斜体`DIV`。 如果您需要处理大量的这种方式中的样式，则时间将会成为一个问题。

以下过程包含可用于轻松地处理 HTML 文档和元素的样式的代码。 该过程要求你知道如何在 Windows 窗体，如创建新项目并将控件添加到窗体中执行基本任务。

### <a name="to-process-style-changes-in-a-windows-forms-application"></a>若要处理在 Windows 窗体应用程序中的样式更改

1. 创建新的 Windows 窗体项目。

2. 创建新的类文件适合于您的编程语言的扩展中结束。

3. 复制`StyleGenerator`类到类文件中，在本主题的示例部分中的代码并保存代码。

4. 将以下 HTML 保存到名为 Test.htm 的文件。

    ```html
    <HTML>
        <BODY>

            <DIV style="font-face:arial;font-weight:bold;">
                Hello, world!
            </DIV><P>

            <DIV>
                Hello again, world!
            </DIV><P>

        </BODY>
    </HTML>
    ```

5. 添加<xref:System.Windows.Forms.WebBrowser>名为控件`webBrowser1`到你的项目的主窗体。

6. 将以下代码添加到你的项目的代码文件。

    > [!IMPORTANT]
    >  絋粄`webBrowser1_DocumentCompleted`事件处理程序配置为侦听<xref:System.Windows.Forms.WebBrowser.DocumentCompleted>事件。 在 Visual Studio 中，双击<xref:System.Windows.Forms.WebBrowser>控制; 请在文本编辑器中，以编程方式配置侦听器。  
  
     [!code-csharp[ManagedDOMStyles#2](~/samples/snippets/csharp/VS_Snippets_Winforms/ManagedDOMStyles/CS/Form1.cs#2)]
     [!code-vb[ManagedDOMStyles#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/ManagedDOMStyles/VB/Form1.vb#2)]  
  
7.  运行该项目。 通过在第一个运行光标`DIV`以观察代码的影响。  
  
## <a name="example"></a>示例  
 下面的代码示例演示的完整代码`StyleGenerator`类，该类将现有的样式值的分析，支持添加、 更改和移除样式，并返回新的样式值与所请求的更改。  
  
 [!code-csharp[ManagedDOMStyles#1](~/samples/snippets/csharp/VS_Snippets_Winforms/ManagedDOMStyles/CS/StyleGenerator.cs#1)]
 [!code-vb[ManagedDOMStyles#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/ManagedDOMStyles/VB/StyleGenerator.vb#1)]  
  
## <a name="see-also"></a>请参阅

- <xref:System.Windows.Forms.HtmlElement>
