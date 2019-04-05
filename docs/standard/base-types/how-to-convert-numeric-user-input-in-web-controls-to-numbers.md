---
title: 如何：将用户在 Web 控件中输入的数值转换成数字
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- numeric format strings [.NET Framework]
- formatting [.NET Framework], numbers
- number formatting [.NET Framework]
- parsing strings [.NET Framework], numeric strings
- converting numeric user input to number
- numbers [.NET Framework], converting numeric user input to number
ms.assetid: f27ddfb8-7479-4b79-8879-02a3bd8402d4
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c66235d866bd7c276d049d9415015dd6f9aa9fb6
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54722356"
---
# <a name="how-to-convert-numeric-user-input-in-web-controls-to-numbers"></a>如何：将用户在 Web 控件中输入的数值转换成数字
由于世界各地的人都可以查看网页，因此用户能够在 <xref:System.Web.UI.WebControls.TextBox> 控件中以几乎无限种格式输入数字数据。 所以，请务必确定网页用户的区域设置和区域性。 分析用户输入后，可以应用用户的区域设置和区域性定义的格式设置约定。  
  
### <a name="to-convert-numeric-input-from-a-web-textbox-control-to-a-number"></a>将 Web 文本框控件中的数字输入转换为数字的具体步骤  
  
1.  确定是否已填充 <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=nameWithType> 属性返回的字符串数组。 如果没有，请继续执行第 6 步。  
  
2.  如果已填充 <xref:System.Web.HttpRequest.UserLanguages%2A> 属性返回的字符串数组，请检索其中第一个元素。 第一个元素指明用户的默认或首选语言和区域。  
  
3.  通过调用 <xref:System.Globalization.CultureInfo.%23ctor%28System.String%2CSystem.Boolean%29?displayProperty=nameWithType> 构造函数，实例化表示用户首选区域性的 <xref:System.Globalization.CultureInfo> 对象。  
  
4.  调用要将用户输入转换为的数字类型的 `TryParse` 或 `Parse` 方法。 重载 `TryParse` 或 `Parse` 方法（带 `provider` 参数），并将它传递到下面两个对象之一：  
  
    -   第 3 步中创建的 <xref:System.Globalization.CultureInfo> 对象。  
  
    -   第 3 步中创建的 <xref:System.Globalization.CultureInfo> 对象的 <xref:System.Globalization.CultureInfo.NumberFormat%2A> 属性返回的 <xref:System.Globalization.NumberFormatInfo> 对象。  
  
5.  如果转换失败，请对 <xref:System.Web.HttpRequest.UserLanguages%2A> 属性返回的字符串数组中的每个剩余元素重复执行第 2 步到第 4 步。  
  
6.  如果转换仍失败或 <xref:System.Web.HttpRequest.UserLanguages%2A> 属性返回的字符串数组为空，请使用 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> 属性返回的固定区域性分析字符串。  
  
## <a name="example"></a>示例  
 下面的示例是 Web 窗体的完整代码隐藏页面，此窗体提示用户在 <xref:System.Web.UI.WebControls.TextBox> 控件中输入数值，并将它转换为数字。 然后，使用与原始输入相同的格式设置规则，加倍并显示数字。  
  
 [!code-csharp[Formatting.HowTo.ParseNumericInput#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.ParseNumericInput/cs/NumericUserInput1.aspx.cs#1)]
 [!code-vb[Formatting.HowTo.ParseNumericInput#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.ParseNumericInput/vb/NumericUserInput1.aspx.vb#1)]  
  
 <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=nameWithType> 属性使用 HTTP 请求头 `Accept-Language` 中的区域性名称进行填充。 不过，并非所有浏览器都有请求头 `Accept-Language`，而且用户还可以完全取消头。 因此，分析用户输入时，务必要有回退区域性。 通常情况下，回退区域性是 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> 返回的固定区域性。 用户还可以向 Internet Explorer 提供在文本框中输入的区域性名称。这样一来，区域性名称就有可能是无效的。 因此，实例化 <xref:System.Globalization.CultureInfo> 对象时，请务必使用异常处理。  
  
 从 Internet Explorer 提交的 HTTP 请求中检索内容时，<xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=nameWithType> 数组按用户首选项顺序进行填充。 数组中的第一个元素包含用户的主要区域性/区域名称。 如果数组包含其他任何项，Internet Explorer 会向它们随意分配质量说明符（通过分号与区域性名称隔开）。 例如，fr-FR 区域性条目可能会采用 `fr-FR;q=0.7` 格式。  
  
 此示例调用 `useUserOverride` 参数设置为 `false` 的 <xref:System.Globalization.CultureInfo.%23ctor%2A> 构造函数，以新建 <xref:System.Globalization.CultureInfo> 对象。 这样可确保在区域性名称是服务器上的默认区域性名称时，类构造函数新建的 <xref:System.Globalization.CultureInfo> 对象包含区域性默认设置，并不反映使用服务器的“区域和语言选项”应用重写的任何设置。 服务器上任何已重写设置的值既不太可能存在于用户系统中，也不太可能反映在用户输入中。  
  
 代码可以调用用户输入将转换为的数字类型的 `Parse` 或 `TryParse` 方法。 一个分析操作可能需要重复调用分析方法。 因此，`TryParse` 方法更好，因为如果分析操作失败，它可以返回 `false`。 相比之下，如果在 Web 应用中处理 `Parse` 方法可能会重复抛出的异常，成本可能会非常高。  
  
## <a name="compiling-the-code"></a>编译代码  
 若要编译代码，请将它复制到 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 代码隐藏页面中，以便替换所有现有代码。 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 网页应包含以下控件：  
  
-   未在代码中引用的 <xref:System.Web.UI.WebControls.Label> 控件。 将它的 <xref:System.Web.UI.WebControls.TextBox.Text%2A> 属性设置为“Enter a Number:”。  
  
-   名为 `NumericString` 的 <xref:System.Web.UI.WebControls.TextBox> 控件。  
  
-   名为 `OKButton` 的 <xref:System.Web.UI.WebControls.Button> 控件。 将它的 <xref:System.Web.UI.WebControls.Button.Text%2A> 属性设置为“OK”。  
  
 将类名从 `NumericUserInput` 更改为 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 页面上 `Page` 指令的 `Inherits` 属性定义的类名。 将 `NumericInput` 对象引用名称更改为 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 页面上 `form` 标记的 `id` 属性定义的名称。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 为防止用户向 HTML 流注入脚本，不得在服务器响应中直接回显用户输入。 相反，应使用 <xref:System.Web.HttpServerUtility.HtmlEncode%2A?displayProperty=nameWithType> 方法进行回显。  
  
## <a name="see-also"></a>请参阅

- [执行格式设置操作](../../../docs/standard/base-types/performing-formatting-operations.md)
- [分析数值字符串](../../../docs/standard/base-types/parsing-numeric.md)
