---
title: 如何：在 Visual Basic 中记录异常
ms.date: 07/20/2015
helpviewer_keywords:
- exceptions, logging
- exceptions, tracking
ms.assetid: a26c60e2-ae39-444a-aebb-33eccadc0eeb
ms.openlocfilehash: 10d1d25f830ff563cf70369e7b9d4c66f639c121
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56969786"
---
# <a name="how-to-log-exceptions-in-visual-basic"></a>如何：在 Visual Basic 中记录异常
可以使用 `My.Application.Log` 和 `My.Log` 对象来记录有关应用程序中所发生异常的信息。 这些示例演示如何使用 `My.Application.Log.WriteException` 方法来记录显式捕获的异常和未处理的异常。  
  
 若要记录跟踪信息，请使用 `My.Application.Log.WriteEntry` 方法。 有关详细信息，请参阅<xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A>。  
  
### <a name="to-log-a-handled-exception"></a>记录已处理的异常  
  
1.  创建将生成异常信息的方法。  
  
     [!code-vb[VbVbalrMyApplicationLog#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#9)]  
  
2.  使用 `Try...Catch` 块捕获该异常。  
  
     [!code-vb[VbVbalrMyApplicationLog#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#6)]  
  
3.  将可能生成异常的代码置于 `Try` 块中。  
  
     取消注释 `Dim` 和 `MsgBox` 行，导致 <xref:System.NullReferenceException> 异常。  
  
     [!code-vb[VbVbalrMyApplicationLog#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#7)]  
  
4.  在 `Catch` 块中，使用 `My.Application.Log.WriteException` 方法写入异常信息。  
  
     [!code-vb[VbVbalrMyApplicationLog#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#8)]  
  
     下面的示例演示用于记录已处理的异常的完整代码。  
  
     [!code-vb[VbVbalrMyApplicationLog#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#10)]  
  
### <a name="to-log-an-unhandled-exception"></a>记录未处理的异常  
  
1.  在 “解决方案资源管理器”中选择一个项目。 在 **“项目”** 菜单上，选择 **“属性”**。  
  
2.  单击“应用程序”  选项卡。  
  
3.  单击“查看应用程序事件”  按钮，打开“代码编辑器”。  
  
     此时将打开 ApplicationEvents.vb 文件。  
  
4.  在“代码编辑器”中打开 ApplicationEvents.vb 文件。 在“常规”  菜单上，选择“MyApplication 事件”。  
  
5.  在“声明”菜单上，选择“UnhandledException”。  
  
     在主应用程序运行之前，应用程序将引发 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException> 事件。  
  
6.  将 `My.Application.Log.WriteException` 方法添加到 `UnhandledException` 事件处理程序。  
  
     [!code-vb[VbVbalrMyApplicationLog#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/MyEventsFake.vb#4)]  
  
     下面的示例演示用于记录未处理的异常的完整代码。  
  
     [!code-vb[VbVbalrMyApplicationLog#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/MyEventsFake.vb#5)]  
  
## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteException%2A>
- [使用应用程序日志](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)
- [如何：写入日志消息](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-log-messages.md)
- [演练：确定 My.Application.Log 在哪里写入信息](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md)
- [演练：更改 My.Application.Log 在哪里写入信息](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-changing-where-my-application-log-writes-information.md)
