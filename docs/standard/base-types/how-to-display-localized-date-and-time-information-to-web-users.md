---
title: 如何：向 Web 用户显示本地化的日期和时间信息
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- formatting [.NET Framework], dates
- parsing strings [.NET Framework], date and time strings
- localization [.NET Framework], date and time displays
- formatting [.NET Framework], localized data
- displaying date and time data
- localized date displays [.NET Framework]
ms.assetid: 377fe93c-32be-421a-a30a-be639a46ede8
dev_langs:
- csharp
- vb
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d46b2634096cf71701458ca7ecb6f66a01ebffbe
ms.sourcegitcommit: 5dcfeb59179e81071f54840d4902cbe00b184294
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2019
ms.locfileid: "54857653"
---
# <a name="how-to-display-localized-date-and-time-information-to-web-users"></a>如何：向 Web 用户显示本地化的日期和时间信息
由于世界各地的人都可以查看网页，因此在与用户交互时，分析和设置日期和时间值的格式的操作不得依赖默认格式（通常是 Web 服务器本地区域性的格式）。 相反，处理用户输入的日期和时间字符串的 Web 窗体，应使用用户的首选区域性分析字符串。 同样，日期和时间数据应以符合用户区域性的格式向用户显示。 本主题演示如何执行此操作。  
  
## <a name="to-parse-date-and-time-strings-input-by-the-user"></a>分析用户输入的日期和时间字符串的具体步骤  
  
1.  确定是否已填充 <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=nameWithType> 属性返回的字符串数组。 如果没有，请继续执行第 6 步。  
  
2.  如果已填充 <xref:System.Web.HttpRequest.UserLanguages%2A> 属性返回的字符串数组，请检索其中第一个元素。 第一个元素指明用户的默认或首选语言和区域。  
  
3.  通过调用 <xref:System.Globalization.CultureInfo.%23ctor%28System.String%2CSystem.Boolean%29?displayProperty=nameWithType> 构造函数，实例化表示用户首选区域性的 <xref:System.Globalization.CultureInfo> 对象。  
  
4.  调用 <xref:System.DateTime> 或 <xref:System.DateTimeOffset> 类型的 `TryParse` 或 `Parse` 方法，尝试执行转换。 重载 `TryParse` 或 `Parse` 方法（带 `provider` 参数），并将它传递到下面两个对象之一：  
  
    -   第 3 步中创建的 <xref:System.Globalization.CultureInfo> 对象。  
  
    -   第 3 步中创建的 <xref:System.Globalization.CultureInfo> 对象的 <xref:System.Globalization.CultureInfo.DateTimeFormat%2A> 属性返回的 <xref:System.Globalization.DateTimeFormatInfo> 对象。  
  
5.  如果转换失败，请对 <xref:System.Web.HttpRequest.UserLanguages%2A> 属性返回的字符串数组中的每个剩余元素重复执行第 2 步到第 4 步。  
  
6.  如果转换仍失败或 <xref:System.Web.HttpRequest.UserLanguages%2A> 属性返回的字符串数组为空，请使用 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> 属性返回的固定区域性分析字符串。  
  
## <a name="to-parse-the-local-date-and-time-of-the-users-request"></a>分析用户请求的本地日期和时间的具体步骤  
  
1.  向 Web 窗体添加 <xref:System.Web.UI.WebControls.HiddenField> 控件。  
  
2.  通过将当前日期和时间以及本地时区与协调世界时 (UTC) 的偏移写入 <xref:System.Web.UI.WebControls.HiddenField.Value%2A> 属性，创建用于处理 `Submit` 按钮的 `onClick` 事件的 JavaScript 函数。 使用分隔符（如分号）将字符串的两个组成部分分开。  
  
3.  使用 Web 窗体的 <xref:System.Web.UI.Control.PreRender> 事件，通过将脚本文本传递给 <xref:System.Web.UI.ClientScriptManager.RegisterClientScriptBlock%28System.Type%2CSystem.String%2CSystem.String%2CSystem.Boolean%29?displayProperty=nameWithType> 方法，将函数注入 HTML 输出流中。  
  
4.  通过将 JavaScript 函数名称提供给 `Submit` 按钮的 `OnClientClick` 属性，将事件处理程序连接到 `Submit` 按钮的 `onClick` 事件。  
  
5.  创建 `Submit` 按钮的 <xref:System.Web.UI.WebControls.Button.Click> 事件的处理程序。  
  
6.  在事件处理程序中，确定是否已填充 <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=nameWithType> 属性返回的字符串数组。 如果没有，请继续执行第 14 步。  
  
7.  如果已填充 <xref:System.Web.HttpRequest.UserLanguages%2A> 属性返回的字符串数组，请检索其中第一个元素。 第一个元素指明用户的默认或首选语言和区域。  
  
8.  通过调用 <xref:System.Globalization.CultureInfo.%23ctor%28System.String%2CSystem.Boolean%29?displayProperty=nameWithType> 构造函数，实例化表示用户首选区域性的 <xref:System.Globalization.CultureInfo> 对象。  
  
9. 将分配给 <xref:System.Web.UI.WebControls.HiddenField.Value%2A> 属性的字符串传递给 <xref:System.String.Split%2A> 方法，以将用户的本地日期和时间的字符串表示形式以及用户的本地时区偏移的字符串表示形式存储到单独的数组元素中。  
  
10. 调用 <xref:System.DateTime.Parse%2A?displayProperty=nameWithType> 或 <xref:System.DateTime.TryParse%28System.String%2CSystem.IFormatProvider%2CSystem.Globalization.DateTimeStyles%2CSystem.DateTime%40%29?displayProperty=nameWithType> 方法，将用户请求的日期和时间转换为 <xref:System.DateTime> 值。 重载方法（带 `provider` 参数），并将它传递到下面两个对象之一：  
  
    -   第 8 步中创建的 <xref:System.Globalization.CultureInfo> 对象。  
  
    -   第 8 步中创建的 <xref:System.Globalization.CultureInfo> 对象的 <xref:System.Globalization.CultureInfo.DateTimeFormat%2A> 属性返回的 <xref:System.Globalization.DateTimeFormatInfo> 对象。  
  
11. 如果第 10 步中的分析操作失败，请转到第 13 步。 否则，调用 <xref:System.UInt32.Parse%28System.String%29?displayProperty=nameWithType> 方法，将用户时区偏移的字符串表示形式转换为整数。  
  
12. 通过调用 <xref:System.DateTimeOffset.%23ctor%28System.DateTime%2CSystem.TimeSpan%29?displayProperty=nameWithType> 构造函数，实例化表示用户的本地时间的 <xref:System.DateTimeOffset>。  
  
13. 如果第 10 步中的转换失败，请对 <xref:System.Web.HttpRequest.UserLanguages%2A> 属性返回的字符串数组中的每个剩余元素重复执行第 7 步到第 12 步。  
  
14. 如果转换仍失败或 <xref:System.Web.HttpRequest.UserLanguages%2A> 属性返回的字符串数组为空，请使用 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> 属性返回的固定区域性分析字符串。 然后，重复第 7 步到第 12 步。  
  
 生成的结果是，表示网页的用户本地时间的 <xref:System.DateTimeOffset> 对象。 然后，可以通过调用 <xref:System.DateTimeOffset.ToUniversalTime%2A> 方法来确定相当 UTC。 还可以调用 <xref:System.TimeZoneInfo.ConvertTime%28System.DateTimeOffset%2CSystem.TimeZoneInfo%29?displayProperty=nameWithType> 方法，并将 <xref:System.TimeZoneInfo.Local%2A?displayProperty=nameWithType> 值作为要将时间转换到的时区进行传递，确定 Web 服务器上的相当日期和时间。  
  
## <a name="example"></a>示例  
 下面的示例包含 HTML 源和 ASP.NET Web 窗体代码，窗体提示用户输入日期和时间值。 客户端脚本还会在隐藏字段中写入以下信息：用户请求的本地日期和时间，以及用户时区与 UTC 的偏移。 然后，服务器会分析此类信息，返回显示用户输入的网页。 它还使用用户的本地时间、服务器上的时间和 UTC，显示用户请求的日期和时间。  
  
 [!code-aspx-csharp[Formatting.HowTo.ParseDateInput#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.ParseDateInput/cs/GetDateInfo.aspx#1)]
 [!code-aspx-vb[Formatting.HowTo.ParseDateInput#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.ParseDateInput/vb/GetDateInfo.aspx#1)]
  
 客户端脚本调用 JavaScript `toLocaleString` 方法。 这会生成遵循用户区域设置的格式设置约定的字符串（更有可能在服务器上成功分析）。  
  
 <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=nameWithType> 属性使用 HTTP 请求头 `Accept-Language` 中的区域性名称进行填充。 不过，并非所有浏览器都有请求头 `Accept-Language`，而且用户还可以完全取消头。 因此，分析用户输入时，务必要有回退区域性。 通常情况下，回退区域性是 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> 返回的固定区域性。 用户还可以向 Internet Explorer 提供在文本框中输入的区域性名称。这样一来，区域性名称就有可能是无效的。 因此，实例化 <xref:System.Globalization.CultureInfo> 对象时，请务必使用异常处理。  
  
 从 Internet Explorer 提交的 HTTP 请求中检索内容时，<xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=nameWithType> 数组按用户首选项顺序进行填充。 数组中的第一个元素包含用户的主要区域性/区域名称。 如果数组包含其他任何项，Internet Explorer 会向它们随意分配质量说明符（通过分号与区域性名称隔开）。 例如，fr-FR 区域性条目可能会采用 `fr-FR;q=0.7` 格式。  
  
 此示例调用 `useUserOverride` 参数设置为 `false` 的 <xref:System.Globalization.CultureInfo.%23ctor%2A> 构造函数，以新建 <xref:System.Globalization.CultureInfo> 对象。 这样可确保在区域性名称是服务器上的默认区域性名称时，类构造函数新建的 <xref:System.Globalization.CultureInfo> 对象包含区域性默认设置，并不反映使用服务器的“区域和语言选项”应用重写的任何设置。 服务器上任何已重写设置的值既不太可能存在于用户系统中，也不太可能反映在用户输入中。  
  
 因为此示例分析日期和时间的两个字符串表示形式（一个由用户输入，另一个存储到隐藏字段），所以它定义了可能提前需要的 <xref:System.Globalization.CultureInfo> 对象。 它会创建 <xref:System.Globalization.CultureInfo> 对象数组，比 <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=nameWithType> 属性返回的元素数量多一个。 然后，它为每个语言/区域字符串实例化 <xref:System.Globalization.CultureInfo> 对象，并实例化表示 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> 的 <xref:System.Globalization.CultureInfo> 对象。  
  
 代码可以调用 <xref:System.DateTime.Parse%2A> 或 <xref:System.DateTime.TryParse%2A> 方法，将用户的日期和时间字符串表示形式转换为 <xref:System.DateTime> 值。 一个分析操作可能需要重复调用分析方法。 因此，<xref:System.DateTime.TryParse%2A> 方法更好，因为如果分析操作失败，它可以返回 `false`。 相比之下，如果在 Web 应用中处理 <xref:System.DateTime.Parse%2A> 方法可能会重复抛出的异常，成本可能会非常高。  
  
## <a name="compiling-the-code"></a>编译代码  
 若要编译代码，请创建没有代码隐藏的 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 网页。 然后，将示例复制到网页中，用它替换所有现有代码。 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 网页应包含以下控件：  
  
-   未在代码中引用的 <xref:System.Web.UI.WebControls.Label> 控件。 将它的 <xref:System.Web.UI.WebControls.TextBox.Text%2A> 属性设置为“Enter a Number:”。  
  
-   名为 `DateString` 的 <xref:System.Web.UI.WebControls.TextBox> 控件。  
  
-   名为 `OKButton` 的 <xref:System.Web.UI.WebControls.Button> 控件。 将它的 <xref:System.Web.UI.WebControls.Button.Text%2A> 属性设置为“OK”。  
  
-   名为 `DateInfo` 的 <xref:System.Web.UI.WebControls.HiddenField> 控件。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 为防止用户向 HTML 流注入脚本，不得在服务器响应中直接回显用户输入。 相反，应使用 <xref:System.Web.HttpServerUtility.HtmlEncode%2A?displayProperty=nameWithType> 方法进行回显。  
  
## <a name="see-also"></a>请参阅

- [执行格式设置操作](../../../docs/standard/base-types/performing-formatting-operations.md)
- [标准日期和时间格式字符串](../../../docs/standard/base-types/standard-date-and-time-format-strings.md)
- [自定义日期和时间格式字符串](../../../docs/standard/base-types/custom-date-and-time-format-strings.md)
- [分析日期和时间字符串](../../../docs/standard/base-types/parsing-datetime.md)
