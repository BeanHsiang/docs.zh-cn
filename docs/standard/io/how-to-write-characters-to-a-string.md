---
title: 如何：向字符串写入字符
ms.date: 01/21/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data streams, writing characters to string
- writing characters to strings
- streams, writing characters to strings
- I/O [.NET Framework], writing characters to strings
ms.assetid: 1222cbeb-0760-44bf-9888-914a2a37174b
author: mairaw
ms.author: mairaw
ms.openlocfilehash: eb35c61b34fa571f35da6691ebe7fa2516eb2df1
ms.sourcegitcommit: b8ace47d839f943f785b89e2fff8092b0bf8f565
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2019
ms.locfileid: "55674745"
---
# <a name="how-to-write-characters-to-a-string"></a>如何：向字符串写入字符
下面的代码示例从字符数组以同步或异步方式向字符串写入字符。  
  
## <a name="example-write-characters-synchronously-in-a-console-app"></a>示例:在控制台应用中以同步方式编写字符  
 下面的示例使用 <xref:System.IO.StringWriter> 将五个字符同步写入 <xref:System.Text.StringBuilder> 对象。 
  
 [!code-csharp[Conceptual.StringBuilder#9](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/example2.cs#9)]
 [!code-vb[Conceptual.StringBuilder#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/example2.vb#9)]  
  
## <a name="example-write-characters-asynchronously-in-a-wpf-app"></a>示例:在 WPF 应用中异步写入字符 
 下一个示例是 WPF 应用背后的代码。 在窗口加载时，示例从 <xref:System.Windows.Controls.TextBox> 控件异步读取所有字符，并将其存储在数组中。 随后，它以异步方式将每个字母或空格字符写入单独的 <xref:System.Windows.Controls.TextBlock> 控件行。  
  
 [!code-csharp[StreamReaderWriter](../../../samples/snippets/csharp/VS_Snippets_Wpf/StringReaderWriter/MainWindow.xaml.cs)]
 [!code-vb[StreamReaderWriter](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StringReaderWriter/MainWindow.xaml.vb)]  
  
## <a name="see-also"></a>请参阅

- <xref:System.IO.StringWriter>  
- <xref:System.IO.StringWriter.Write%2A?displayProperty=nameWithType>  
- <xref:System.Text.StringBuilder>  
- [文件和流 I/O](../../../docs/standard/io/index.md)  
- [异步文件 I/O](../../../docs/standard/io/asynchronous-file-i-o.md)  
- [如何：枚举目录和文件](../../../docs/standard/io/how-to-enumerate-directories-and-files.md)  
- [如何：对新建的数据文件进行读取和写入](../../../docs/standard/io/how-to-read-and-write-to-a-newly-created-data-file.md)  
- [如何：打开并追加到日志文件](../../../docs/standard/io/how-to-open-and-append-to-a-log-file.md)  
- [如何：从文件中读取文本](../../../docs/standard/io/how-to-read-text-from-a-file.md)  
- [如何：将文本写入文件](../../../docs/standard/io/how-to-write-text-to-a-file.md)  
- [如何：从字符串中读取字符](../../../docs/standard/io/how-to-read-characters-from-a-string.md)
