---
title: 如何：诊断有问题的打印作业
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- troubleshooting print job problems [WPF]
- print jobs [WPF], troubleshooting
- print jobs [WPF], diagnosing problems
ms.assetid: b081a170-84c6-48f9-a487-5766a8d58a82
ms.openlocfilehash: babd601bb29fc2aa9c906921082a18942f6649c0
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57369703"
---
# <a name="how-to-diagnose-problematic-print-job"></a>如何：诊断有问题的打印作业
网络管理员经常接收到有关打印作业无法打印或打印速度慢的用户投诉。 丰富的打印作业属性中公开[!INCLUDE[TLA#tla_api#plural](../../../../includes/tlasharptla-apisharpplural-md.md)]的 Microsoft.NET Framework 提供了一种方法用于执行快速的打印作业远程诊断。  
  
## <a name="example"></a>示例  
 以下是创建此类实用程序的主要步骤。  
  
1.  标识用户投诉的打印作业。 用户通常无法准确完成此操作。 他们可能不知道打印服务器或打印机的名称。 它们可能不是设置中使用的描述不同的术语中的打印机的位置及其<xref:System.Printing.PrintQueue.Location%2A>属性。 这样的话，一个好办法是生成用户当前所提交作业的列表。 如果存在多个作业，则可通过用户和打印系统管理员之间的通信来查明出现问题的作业。 子步骤如下。  
  
    1.  获取所有打印服务器的列表。  
  
    2.  循环访问服务器以查询其打印队列。  
  
    3.  在每一轮服务器循环访问过程中，循环访问所有服务器的队列，以查询其作业  
  
    4.  在每一轮服务器循环访问过程中，循环访问其作业，并收集与投诉用户已提交的作业相关的标识信息。  
  
2.  当已识别有问题的打印作业时，检查相关属性以查明可能的问题。 例如，作业是否处于错误状态，或服务于队列的打印机是否在打印该作业之前处于脱机状态？  
  
 以下代码是一系列代码示例。 第一个代码示例包含针对打印队列的循环访问操作。 （以上步骤 1c。）在变量`myPrintQueues`是<xref:System.Printing.PrintQueueCollection>当前打印服务器对象。  
  
 该代码示例开始先刷新当前打印队列对象与<xref:System.Printing.PrintQueue.Refresh%2A?displayProperty=nameWithType>。 这可确保该对象的属性能够准确表示它所表示的物理打印机的状态。 然后，应用程序获取打印作业的集合当前打印队列中通过使用<xref:System.Printing.PrintQueue.GetPrintJobInfoCollection%2A>。  
  
 接下来，应用程序会遍历<xref:System.Printing.PrintSystemJobInfo>集合进行比较每个<xref:System.Printing.PrintSystemJobInfo.Submitter%2A>属性与投诉用户的别名。 如果属性和别名相匹配，则应用程序会将有关该作业的标识信息添加到将呈现的字符串。 （`userName` 和 `jobList` 变量在应用程序早期进行初始化。）  
  
 [!code-cpp[DiagnoseProblematicPrintJob#EnumerateJobsInQueues](~/samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#enumeratejobsinqueues)]
 [!code-csharp[DiagnoseProblematicPrintJob#EnumerateJobsInQueues](~/samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#enumeratejobsinqueues)]
 [!code-vb[DiagnoseProblematicPrintJob#EnumerateJobsInQueues](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#enumeratejobsinqueues)]  
  
 下一代码示例在步骤 2 提取应用程序。 （请参阅上文。）已标识有问题的作业，应用程序会提示提供用于标识该作业的信息。 此信息从它创建<xref:System.Printing.PrintServer>， <xref:System.Printing.PrintQueue>，和<xref:System.Printing.PrintSystemJobInfo>对象。  
  
 此时，应用程序包含一个分支结构，该结构对应于检查打印作业状态的两种方法：  
  
-   可以读取的标志<xref:System.Printing.PrintSystemJobInfo.JobStatus%2A>属性的类型即<xref:System.Printing.PrintJobStatus>。  
  
-   你可以读取每个相关属性，如<xref:System.Printing.PrintSystemJobInfo.IsBlocked%2A>和<xref:System.Printing.PrintSystemJobInfo.IsInError%2A>。  
  
 此示例演示这两种方法，因此该用户之前进行提示要使用的方法并回复"Y"，如果他或她想要使用的标志<xref:System.Printing.PrintSystemJobInfo.JobStatus%2A>属性。 请参阅以下有关这两种方法的详细信息。 最后，该应用程序使用一种名为 **ReportQueueAndJobAvailability** 的方法来报告是否可以在一天的此时打印该作业。 [确定此时是否可以打印一项打印作业](how-to-discover-whether-a-print-job-can-be-printed-at-this-time-of-day.md)中就此方法进行了讨论。  
  
 [!code-cpp[DiagnoseProblematicPrintJob#IdentifyAndDiagnoseProblematicJob](~/samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#identifyanddiagnoseproblematicjob)]
 [!code-csharp[DiagnoseProblematicPrintJob#IdentifyAndDiagnoseProblematicJob](~/samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#identifyanddiagnoseproblematicjob)]
 [!code-vb[DiagnoseProblematicPrintJob#IdentifyAndDiagnoseProblematicJob](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#identifyanddiagnoseproblematicjob)]  
  
 若要使用的标志检查打印作业状态<xref:System.Printing.PrintSystemJobInfo.JobStatus%2A>属性，检查每个相关标志以查看它是否设置。 检查是否在一组位标志中设置了一个位的标准方法是执行一个逻辑 AND 运算，其中将该组标志作为一个操作数，将标志本身作为另一操作数。 由于该标志本身仅设置一个位，因此逻辑 AND 的结果至多为设置了该相同位。 若要查明事实是否如此，只需将逻辑 AND 的结果与标志本身进行比较。 有关详细信息，请参阅<xref:System.Printing.PrintJobStatus>，则[& 运算符 (C#引用)](~/docs/csharp/language-reference/operators/and-operator.md)，并<xref:System.FlagsAttribute>。  
  
 对于已设置了其位的每个属性，代码会将此报告给控制台屏幕，有时还会建议如何响应。 （下面讨论了作业或队列暂停时所调用的 **HandlePausedJob** 方法。）  
  
 [!code-cpp[DiagnoseProblematicPrintJob#SpotTroubleUsingJobAttributes](~/samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#spottroubleusingjobattributes)]
 [!code-csharp[DiagnoseProblematicPrintJob#SpotTroubleUsingJobAttributes](~/samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#spottroubleusingjobattributes)]
 [!code-vb[DiagnoseProblematicPrintJob#SpotTroubleUsingJobAttributes](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#spottroubleusingjobattributes)]  
  
 若要使用单独的属性检查打印作业状态，只需读取每个属性，如果属性为 `true`，则报告给控制台屏幕，并建议一种可能的响应方式。 （下面讨论了作业或队列暂停时所调用的 **HandlePausedJob** 方法。）  
  
 [!code-cpp[DiagnoseProblematicPrintJob#SpotTroubleUsingJobProperties](~/samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#spottroubleusingjobproperties)]
 [!code-csharp[DiagnoseProblematicPrintJob#SpotTroubleUsingJobProperties](~/samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#spottroubleusingjobproperties)]
 [!code-vb[DiagnoseProblematicPrintJob#SpotTroubleUsingJobProperties](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#spottroubleusingjobproperties)]  
  
 使用 **HandlePausedJob** 方法，应用程序的用户能够远程恢复暂停的作业。 由于可能存在一个充分的暂停打印队列的理由，因此该方法会首先提示用户是否确实要恢复该作业。 如果回答是"Y"，则<xref:System.Printing.PrintQueue.Resume%2A?displayProperty=nameWithType>调用方法。  
  
 接下来，系统会提示用户是否确实要继续执行作业，这么做是考虑到这个作业可能是独立于队列中的其他作业被单独暂停的。 (比较<xref:System.Printing.PrintQueue.IsPaused%2A?displayProperty=nameWithType>和<xref:System.Printing.PrintSystemJobInfo.IsPaused%2A?displayProperty=nameWithType>。)如果答案为"Y"，则<xref:System.Printing.PrintSystemJobInfo.Resume%2A?displayProperty=nameWithType>被调用; 否则为<xref:System.Printing.PrintSystemJobInfo.Cancel%2A>调用。  
  
 [!code-cpp[DiagnoseProblematicPrintJob#HandlePausedJob](~/samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#handlepausedjob)]
 [!code-csharp[DiagnoseProblematicPrintJob#HandlePausedJob](~/samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#handlepausedjob)]
 [!code-vb[DiagnoseProblematicPrintJob#HandlePausedJob](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#handlepausedjob)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Printing.PrintJobStatus>
- <xref:System.Printing.PrintSystemJobInfo>
- <xref:System.FlagsAttribute>
- <xref:System.Printing.PrintQueue>
- [& 运算符 (C#引用)](~/docs/csharp/language-reference/operators/and-operator.md)
- [WPF 中的文档](documents-in-wpf.md)
- [打印概述](printing-overview.md)
