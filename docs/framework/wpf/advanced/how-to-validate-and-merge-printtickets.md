---
title: 如何：验证和合并 PrintTicket
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- merging PrintTickets [WPF]
- PrintTicket [WPF], merging
- validation of PrintTickets [WPF]
- PrintTicket [WPF], validation
ms.assetid: 4fe2d501-d0b0-4fef-86af-6ffe6c162532
ms.openlocfilehash: 2be08f5d3c2cd82e50569a105e3fa15f12ad352c
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57355163"
---
# <a name="how-to-validate-and-merge-printtickets"></a>如何：验证和合并 PrintTicket
[!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)] [打印架构](https://go.microsoft.com/fwlink/?LinkId=186397)包括灵活且可扩展<xref:System.Printing.PrintCapabilities>和<xref:System.Printing.PrintTicket>元素。 前者详细列举的打印设备的功能，后者用于指定设备应如何使用这些功能来处理特定文档、 单个文档或单页的序列。  
  
 典型的应用程序支持打印的任务序列将如下所示。  
  
1.  确定打印机的功能。  
  
2.  配置<xref:System.Printing.PrintTicket>以使用这些功能。  
  
3.  验证<xref:System.Printing.PrintTicket>。  
  
 本文介绍如何执行此操作。  
  
## <a name="example"></a>示例  
 在下面的简单示例中，我们都只希望打印机是否支持双工 — 双面打印。 主要步骤如下所示。  
  
1.  获取<xref:System.Printing.PrintCapabilities>对象与<xref:System.Printing.PrintQueue.GetPrintCapabilities%2A>方法。  
  
2.  测试存在所需的功能。 在以下示例中，我们测试<xref:System.Printing.PrintCapabilities.DuplexingCapability%2A>属性的<xref:System.Printing.PrintCapabilities>沿长边工作表的对象的一张纸的纸张的"翻页"的两面上的打印功能是否存在。 由于<xref:System.Printing.PrintCapabilities.DuplexingCapability%2A>是一个集合，我们将使用`Contains`方法的<xref:System.Collections.ObjectModel.ReadOnlyCollection%601>。  
  
    > [!NOTE]
    >  此步骤不是绝对必需的。 <xref:System.Printing.PrintQueue.MergeAndValidatePrintTicket%2A>使用以下方法将检查每个请求<xref:System.Printing.PrintTicket>针对打印机的功能。 如果打印机不支持请求的功能，打印机驱动程序将替换中的另一个请求<xref:System.Printing.PrintTicket>方法返回。  
  
3.  如果打印机支持双面打印，示例代码会创建<xref:System.Printing.PrintTicket>的要求进行双面打印。 但应用程序未指定每个可能的打印机设置中提供<xref:System.Printing.PrintTicket>元素。 这将浪费的程序员和计划时间。 相反，该代码设置仅进行双面打印请求，然后将合并这<xref:System.Printing.PrintTicket>与某个现有，完全配置且经过验证， <xref:System.Printing.PrintTicket>，在这种情况下，用户的默认<xref:System.Printing.PrintTicket>。  
  
4.  相应地，示例代码会调用<xref:System.Printing.PrintQueue.MergeAndValidatePrintTicket%2A>方法来合并将新的、 最小，<xref:System.Printing.PrintTicket>用户的默认值<xref:System.Printing.PrintTicket>。 这将返回<xref:System.Printing.ValidationResult>，包含新的<xref:System.Printing.PrintTicket>作为其属性之一。  
  
5.  此示例然后测试新<xref:System.Printing.PrintTicket>请求双面打印。 如果是这样，则代码会将其用户的新的默认打印票证。 如果没有执行上述步骤 2，并且打印机不支持双工沿长边，则测试将会造成`false`。 （请参阅上面的说明。）  
  
6.  最后一个重要步骤是将提交到更改<xref:System.Printing.PrintQueue.UserPrintTicket%2A>的属性<xref:System.Printing.PrintQueue>与<xref:System.Printing.PrintQueue.Commit%2A>方法。  
  
 [!code-csharp[PrintTicketManagment#UsingMergeAndValidate](~/samples/snippets/csharp/VS_Snippets_Wpf/PrintTicketManagment/CSharp/printticket.cs#usingmergeandvalidate)]
 [!code-vb[PrintTicketManagment#UsingMergeAndValidate](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PrintTicketManagment/visualbasic/printticket.vb#usingmergeandvalidate)]  
  
 以便可以快速测试此示例中，如下所示的其余部分。 创建项目和命名空间，然后将在本文中的两个代码片段粘贴到命名空间块。  
  
 [!code-csharp[PrintTicketManagment#UIForMergeAndValidatePTUtility](~/samples/snippets/csharp/VS_Snippets_Wpf/PrintTicketManagment/CSharp/printticket.cs#uiformergeandvalidateptutility)]
 [!code-vb[PrintTicketManagment#UIForMergeAndValidatePTUtility](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PrintTicketManagment/visualbasic/printticket.vb#uiformergeandvalidateptutility)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Printing.PrintCapabilities>
- <xref:System.Printing.PrintTicket>
- <xref:System.Printing.PrintServer.GetPrintQueues%2A>
- <xref:System.Printing.PrintServer>
- <xref:System.Printing.EnumeratedPrintQueueTypes>
- <xref:System.Printing.PrintQueue>
- <xref:System.Printing.PrintQueue.GetPrintCapabilities%2A>
- [WPF 中的文档](documents-in-wpf.md)
- [打印概述](printing-overview.md)
- [打印架构](https://go.microsoft.com/fwlink/?LinkId=186397)
