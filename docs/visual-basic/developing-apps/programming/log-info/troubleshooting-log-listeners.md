---
title: 疑难解答：日志侦听器 (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- event logs, troubleshooting
- troubleshooting Visual Basic, event logs
- troubleshooting event logs
ms.assetid: ac6eb760-3d5d-461e-aedd-40599ee22e49
ms.openlocfilehash: f2dba14ed883b428e47b71533bcb51506167fd49
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56979003"
---
# <a name="troubleshooting-log-listeners-visual-basic"></a>疑难解答：日志侦听器 (Visual Basic)
可以使用 `My.Application.Log` 和 `My.Log` 对象来记录有关应用程序中所发生事件的信息。  
  
 要确定哪些日志侦听器接收这些消息，请参阅[演练：确定 My.Application.Log 在哪里写入信息](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md)。  
  
 `Log` 对象可以使用日志筛选来限制其记录的信息量。 如果筛选器配置错误，则日志可能包含错误信息。 有关筛选器的详细信息，请参阅[演练：筛选 My.Application.Log 输出](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-filtering-my-application-log-output.md)。  
  
 但是，如果日志配置不正确，则可能需要有关其当前配置的详细信息。 可通过日志的高级 `TraceSource` 属性获取此信息。  
  
### <a name="to-determine-the-log-listeners-for-the-log-object-in-code"></a>若要确定代码中日志对象的日志侦听器  
  
1.  在代码文件的开头导入 <xref:System.Diagnostics> 命名空间。 有关详细信息，请参阅 [Imports 语句（.NET 命名空间和类型）](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)。  
  
     [!code-vb[VbVbalrMyApplicationLog#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#13)]  
  
2.  创建一个函数，该函数返回由每个日志侦听器的信息组成的字符串。  
  
     [!code-vb[VbVbalrMyApplicationLog#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#14)]  
  
3.  将日志跟踪侦听器的集合传递到 `GetListeners` 函数，并显示返回值。  
  
     [!code-vb[VbVbalrMyApplicationLog#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#19)]  
  
     有关更多信息，请参见<xref:Microsoft.VisualBasic.Logging.Log.TraceSource%2A>。  
  
## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- [使用应用程序日志](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)
- [演练：确定 My.Application.Log 在哪里写入信息](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md)
