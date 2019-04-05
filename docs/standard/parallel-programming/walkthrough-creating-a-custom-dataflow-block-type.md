---
title: 演练：创建自定义数据流块类型
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Task Parallel Library, dataflows
- TPL dataflow library, creating custom dataflow blocks
- dataflow blocks, creating custom in TPL
ms.assetid: a6147146-0a6a-4d9b-ab0f-237b3c1ac691
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 380bcb6d2a2846d09267eeb3a0d637469ce9fba5
ms.sourcegitcommit: a36cfc9dbbfc04bd88971f96e8a3f8e283c15d42
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2019
ms.locfileid: "54221084"
---
# <a name="walkthrough-creating-a-custom-dataflow-block-type"></a>演练：创建自定义数据流块类型
尽管 TPL 数据流库提供了多种可启用各种功能的数据流块类型，但也可以创建自定义块类型。 本文档介绍了如何创建实现自定义行为的数据流块类型。  
  
## <a name="prerequisites"></a>系统必备  
 阅读本文档前，请先阅读[数据流](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)。  

[!INCLUDE [tpl-install-instructions](../../../includes/tpl-install-instructions.md)]
  
## <a name="defining-the-sliding-window-dataflow-block"></a>定义滑动窗口数据流块  
 假设数据流应用要求缓冲输入值，并以滑动窗口方式输出值。 例如，如果输入值为 {0, 1, 2, 3, 4, 5}，且窗口大小为 3，那么滑动窗口数据流块生成输出数组 {0, 1, 2}、{1, 2, 3}、{2, 3, 4} 和 {3, 4, 5}。 下面各部分介绍了两种方式，用于创建实现此自定义行为的数据流块类型。 第一种方式是，使用 <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Encapsulate%2A> 方法将 <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601> 对象和 <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601> 对象的功能合并到一个传播器块中。 第二种方式是，定义派生自 <xref:System.Threading.Tasks.Dataflow.IPropagatorBlock%602> 的类，并结合现有功能执行自定义行为。  
  
## <a name="using-the-encapsulate-method-to-define-the-sliding-window-dataflow-block"></a>使用 Encapsulate 方法定义滑动窗口数据流块  
 下面的示例使用 <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Encapsulate%2A> 方法通过目标和源创建传播器块。 使用传播器块，可以将源块和目标块用作数据的接收方和发送方。  
  
 如果需要自定义数据流功能，但不需要提供其他方法、属性或字段的类型，此方式就很有用。  
  
 [!code-csharp[TPLDataflow_SlidingWindowBlock#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_slidingwindowblock/cs/slidingwindowblock.cs#1)]
 [!code-vb[TPLDataflow_SlidingWindowBlock#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_slidingwindowblock/vb/slidingwindowblock.vb#1)]  
  
## <a name="deriving-from-ipropagatorblock-to-define-the-sliding-window-dataflow-block"></a>派生自 IPropagatorBlock 以定义滑动窗口数据流块  
 下面的示例展示了 `SlidingWindowBlock` 类。 此类派生自 <xref:System.Threading.Tasks.Dataflow.IPropagatorBlock%602>，可用作数据的源和目标。 与上一示例中所述一样，`SlidingWindowBlock` 类是在现有数据流块类型的基础之上构建而成。 不同之处在于，`SlidingWindowBlock` 类还实现了 <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601>、<xref:System.Threading.Tasks.Dataflow.ITargetBlock%601> 和 <xref:System.Threading.Tasks.Dataflow.IDataflowBlock> 接口所需的方法。 这些方法全都将工作转发给预定义的数据流块类型成员。 例如，`Post` 方法将工作转交给也是 <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601> 对象的 `m_target` 数据成员。  
  
 如果需要自定义数据流功能，还需要提供其他方法、属性或字段的类型，此方式就很有用。 例如，`SlidingWindowBlock` 类也派生自 <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601>，这样就可以提供 <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceive%2A> 和 <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceiveAll%2A> 方法了。 `SlidingWindowBlock` 类还具有扩展性，体现在提供 `WindowSize` 属性，以检索滑动窗口中的元素数量。  
  
 [!code-csharp[TPLDataflow_SlidingWindowBlock#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_slidingwindowblock/cs/slidingwindowblock.cs#2)]
 [!code-vb[TPLDataflow_SlidingWindowBlock#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_slidingwindowblock/vb/slidingwindowblock.vb#2)]  
  
## <a name="the-complete-example"></a>完整示例  
 下面的示例显示此演练的完整代码。 它还展示了如何在对块执行写入和读取操作并将结果打印到控制台的方法中使用两个滑动窗口块。  
  
 [!code-csharp[TPLDataflow_SlidingWindowBlock#100](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_slidingwindowblock/cs/slidingwindowblock.cs#100)]
 [!code-vb[TPLDataflow_SlidingWindowBlock#100](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_slidingwindowblock/vb/slidingwindowblock.vb#100)]  
  
## <a name="compiling-the-code"></a>编译代码  
 复制示例代码，并将它粘贴到 Visual Studio 项目中，或粘贴到 `SlidingWindowBlock.cs`（对于 Visual Basic，则为 `SlidingWindowBlock.vb`）文件中，再在 Visual Studio 开发人员命令提示窗口中运行以下命令。  
  
 Visual C#  
  
 **csc.exe /r:System.Threading.Tasks.Dataflow.dll SlidingWindowBlock.cs**  
  
 Visual Basic  
  
 **vbc.exe /r:System.Threading.Tasks.Dataflow.dll SlidingWindowBlock.vb**  

## <a name="see-also"></a>请参阅

- [数据流](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)
