---
title: 如何：将消息写入数据流块和从数据流块读取消息
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Task Parallel Library, dataflows
- TPL dataflow library, reading and writing messages
ms.assetid: 1a9bf078-aa82-46eb-b95a-f87237f028c5
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 638cd917bdb40fa5bbf1cb02857c71a0127d0e3f
ms.sourcegitcommit: a36cfc9dbbfc04bd88971f96e8a3f8e283c15d42
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2019
ms.locfileid: "54221149"
---
# <a name="how-to-write-messages-to-and-read-messages-from-a-dataflow-block"></a>如何：将消息写入数据流块和从数据流块读取消息
本文档介绍如何使用 TPL 数据流库从数据流块写入和读取消息。 TPL 数据流库同时提供用于从数据流块写入和读取消息的同步和异步方法。 本文档使用 <xref:System.Threading.Tasks.Dataflow.BufferBlock%601?displayProperty=nameWithType> 类。 <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> 类将缓冲消息，而且其行为方式与消息源相同，也与消息目标相同。  

[!INCLUDE [tpl-install-instructions](../../../includes/tpl-install-instructions.md)]

## <a name="writing-to-and-reading-from-a-dataflow-block-synchronously"></a>从数据流块同步写入和读取  
 下面的示例使用 <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Post%2A> 方法写入 <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> 数据流块，使用 <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Receive%2A> 方法从同一对象读取。  
  
 [!code-csharp[TPLDataflow_ReadWrite#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_readwrite/cs/dataflowreadwrite.cs#2)]
 [!code-vb[TPLDataflow_ReadWrite#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_readwrite/vb/dataflowreadwrite.vb#2)]  
  
 如以下示例所示，还可以使用 <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceive%2A> 方法从数据流块读取。 <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceive%2A> 方法不会阻止当前线程，而且在偶尔轮询数据时非常有用。  
  
 [!code-csharp[TPLDataflow_ReadWrite#3](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_readwrite/cs/dataflowreadwrite.cs#3)]
 [!code-vb[TPLDataflow_ReadWrite#3](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_readwrite/vb/dataflowreadwrite.vb#3)]  
  
 由于 <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Post%2A> 方法是同步运行的，前面示例中的 <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> 对象会在第二个循环读取数据之前接收所有数据。 下面的示例对第一个示例进行了扩展，使用 <xref:System.Threading.Tasks.Parallel.Invoke%2A> 同时读取和写入消息块。 由于 <xref:System.Threading.Tasks.Parallel.Invoke%2A> 并发执行操作，因此不会按任何特定的顺序将值写入 <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> 对象。  
  
 [!code-csharp[TPLDataflow_ReadWrite#4](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_readwrite/cs/dataflowreadwrite.cs#4)]
 [!code-vb[TPLDataflow_ReadWrite#4](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_readwrite/vb/dataflowreadwrite.vb#4)]  
  
## <a name="writing-to-and-reading-from-a-dataflow-block-asynchronously"></a>从数据流块异步写入和读取  
 下面的示例使用 <xref:System.Threading.Tasks.Dataflow.DataflowBlock.SendAsync%2A> 方法异步写入 <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> 对象，使用 <xref:System.Threading.Tasks.Dataflow.DataflowBlock.ReceiveAsync%2A> 方法从同一对象异步读取。 本示例使用 [async](~/docs/csharp/language-reference/keywords/async.md) 和 [await](~/docs/csharp/language-reference/keywords/await.md) 运算符（Visual Basic 中为 [Async](~/docs/visual-basic/language-reference/modifiers/async.md) 和 [Await](~/docs/visual-basic/language-reference/operators/await-operator.md)）以异步方式向目标块发送数据以及从中读取数据。 必须启用数据流块来推迟消息时，<xref:System.Threading.Tasks.Dataflow.DataflowBlock.SendAsync%2A> 方法很有用。 希望在数据可用时对此数据进行操作时，<xref:System.Threading.Tasks.Dataflow.DataflowBlock.ReceiveAsync%2A> 方法很有用。 有关消息在消息块之间如何传播的详细信息，请参阅[数据流](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)中的“消息传递”一节。  
  
 [!code-csharp[TPLDataflow_ReadWrite#5](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_readwrite/cs/dataflowreadwrite.cs#5)]
 [!code-vb[TPLDataflow_ReadWrite#5](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_readwrite/vb/dataflowreadwrite.vb#5)]  
  
## <a name="a-complete-example"></a>完整示例  
 下面的示例显示本文档的完整代码。  
  
 [!code-csharp[TPLDataflow_ReadWrite#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_readwrite/cs/dataflowreadwrite.cs#1)]
 [!code-vb[TPLDataflow_ReadWrite#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_readwrite/vb/dataflowreadwrite.vb#1)]  
  
## <a name="compiling-the-code"></a>编译代码  
 复制示例代码，并将它粘贴到 Visual Studio 项目中，或粘贴到 `DataflowReadWrite.cs`（对于 Visual Basic，则为 `DataflowReadWrite.vb`）文件中，再在 Visual Studio 开发人员命令提示窗口中运行以下命令。  
  
 Visual C#  
  
 **csc.exe /r:System.Threading.Tasks.Dataflow.dll DataflowReadWrite.cs**  
  
 Visual Basic  
  
 **vbc.exe /r:System.Threading.Tasks.Dataflow.dll DataflowReadWrite.vb**  
  
## <a name="next-steps"></a>后续步骤  
 本示例演示如何直接从消息块读取和写入。 还可以连接数据流块来形成管道（这是数据流块的线性序列）或网络（这是数据流块的图形）。 在管道或网络中，当数据可用时源向目标异步传播数据。 有关创建基本数据流管道的示例，请参阅[演练：创建数据流管道](../../../docs/standard/parallel-programming/walkthrough-creating-a-dataflow-pipeline.md)。 有关创建更复杂的数据流网络的示例，请参阅[演练：在 Windows 窗体应用程序中使用数据流](../../../docs/standard/parallel-programming/walkthrough-using-dataflow-in-a-windows-forms-application.md)。  
  
## <a name="see-also"></a>请参阅

- [数据流](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)
