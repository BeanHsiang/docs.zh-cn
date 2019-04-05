---
title: 如何：枚举打印队列的子集
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- enumerating [WPF], subset of print queues
- print queues [WPF], enumerating subset of
ms.assetid: cc4a1b5b-d46f-4c5e-bc26-22c226e4bee0
ms.openlocfilehash: 7cdd0ebeb03d078a952dd9ffe4d2ed7590417054
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57359479"
---
# <a name="how-to-enumerate-a-subset-of-print-queues"></a>如何：枚举打印队列的子集
负责管理公司范围内的打印机的信息技术 (IT) 专业人员所面临的常见情况是生成具有某些特征的打印机的列表。 提供此功能<xref:System.Printing.PrintServer.GetPrintQueues%2A>方法<xref:System.Printing.PrintServer>对象和<xref:System.Printing.EnumeratedPrintQueueTypes>枚举。  
  
## <a name="example"></a>示例  
 在下面的示例中，代码先创建标志，用于指定我们想要列出的打印队列的特性数组。 在此示例中，我们正在寻找打印队列打印服务器上本地安装并共享。 <xref:System.Printing.EnumeratedPrintQueueTypes>枚举提供了许多其他的值。  
  
 该代码随后创建<xref:System.Printing.LocalPrintServer>对象，一个类派生自<xref:System.Printing.PrintServer>。 本地打印服务器是在其运行应用程序的计算机。  
  
 最后一个重要步骤是将数组传递给<xref:System.Printing.PrintServer.GetPrintQueues%2A>方法。  
  
 最后，会向用户显示结果。  
  
 [!code-cpp[EnumerateSubsetOfPrintQueues#ListSubsetOfPrintQueues](~/samples/snippets/cpp/VS_Snippets_Wpf/EnumerateSubsetOfPrintQueues/CPP/Program.cpp#listsubsetofprintqueues)]
 [!code-csharp[EnumerateSubsetOfPrintQueues#ListSubsetOfPrintQueues](~/samples/snippets/csharp/VS_Snippets_Wpf/EnumerateSubsetOfPrintQueues/CSharp/Program.cs#listsubsetofprintqueues)]
 [!code-vb[EnumerateSubsetOfPrintQueues#ListSubsetOfPrintQueues](~/samples/snippets/visualbasic/VS_Snippets_Wpf/EnumerateSubsetOfPrintQueues/visualbasic/program.vb#listsubsetofprintqueues)]  
  
 您可以扩展此示例通过让`foreach`循环通过每个打印队列的步骤执行进一步筛选。 例如，您可以筛选掉不支持通过循环调用双面打印的打印机每个打印队列的<xref:System.Printing.PrintQueue.GetPrintCapabilities%2A>方法和测试返回的值进行双面打印是否存在。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Printing.PrintServer.GetPrintQueues%2A>
- <xref:System.Printing.PrintServer>
- <xref:System.Printing.LocalPrintServer>
- <xref:System.Printing.EnumeratedPrintQueueTypes>
- <xref:System.Printing.PrintQueue>
- <xref:System.Printing.PrintQueue.GetPrintCapabilities%2A>
- [WPF 中的文档](documents-in-wpf.md)
- [打印概述](printing-overview.md)
- [Microsoft XPS 文档编写器](https://go.microsoft.com/fwlink/?LinkId=147319)
