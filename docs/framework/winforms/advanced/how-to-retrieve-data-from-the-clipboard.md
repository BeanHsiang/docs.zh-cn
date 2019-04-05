---
title: 如何：从剪贴板中检索数据
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- pasting Clipboard data
- Clipboard [Windows Forms], retrieving data
ms.assetid: 99612537-2c8a-449f-aab5-2b3b28d656e7
ms.openlocfilehash: 0ed79197190e9f646b5f94ff56e62b19fe4f366a
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57723850"
---
# <a name="how-to-retrieve-data-from-the-clipboard"></a>如何：从剪贴板中检索数据
<xref:System.Windows.Forms.Clipboard>类提供了可用于与 Windows 操作系统剪贴板功能进行交互的方法。 许多应用程序的数据用作临时存储库使用剪贴板。 例如，文字处理器剪切和粘贴操作期间使用剪贴板。 剪贴板功能也很有用信息传输到另一个应用程序。  
  
 某些应用程序以增加数据有可能使用其他应用程序的数量以多种格式剪贴板上存储数据。 剪贴板格式是用于标识格式的字符串。 使用标识的格式的应用程序可以检索剪贴板上的关联的数据。 <xref:System.Windows.Forms.DataFormats>类提供了供你使用的预定义的格式名称。 此外可以使用自己的格式名称，或使用对象的类型作为其格式。 有关将数据添加到剪贴板的信息，请参阅[如何：将数据添加到剪贴板](how-to-add-data-to-the-clipboard.md)。  
  
 若要确定剪贴板中是否包含特定格式的数据，请使用之一`Contains`*格式*方法或<xref:System.Windows.Forms.Clipboard.GetData%2A>方法。 若要从剪贴板检索数据，请使用之一`Get`*格式*方法或<xref:System.Windows.Forms.Clipboard.GetData%2A>方法。 这些方法都是中的新增功能[!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)]。  
  
 从通过使用版本剪贴板访问数据早于[!INCLUDE[dnprdnlong](../../../../includes/dnprdnlong-md.md)]，使用<xref:System.Windows.Forms.Clipboard.GetDataObject%2A>方法调用的方法所返回的<xref:System.Windows.Forms.IDataObject>。 若要确定特定的格式是否可在返回的对象，例如，调用<xref:System.Windows.Forms.IDataObject.GetDataPresent%2A>方法。  
  
> [!NOTE]
>  所有基于 Windows 的应用程序共享系统剪贴板。 因此，可能会有所变动时切换到另一个应用程序。  
>   
>  <xref:System.Windows.Forms.Clipboard>类仅可在线程设置为单线程单元 (STA) 模式。 若要使用此类，请确保你`Main`方法将标有<xref:System.STAThreadAttribute>属性。  
  
### <a name="to-retrieve-data-from-the-clipboard-in-a-single-common-format"></a>若要从单个的常见格式在剪贴板中检索数据  
  
1.  使用<xref:System.Windows.Forms.Clipboard.GetAudioStream%2A>， <xref:System.Windows.Forms.Clipboard.GetFileDropList%2A>， <xref:System.Windows.Forms.Clipboard.GetImage%2A>，或<xref:System.Windows.Forms.Clipboard.GetText%2A>方法。 （可选） 使用的相应`Contains`*格式*首先确定数据是否采用特定格式的方法。 这些方法是仅适用于[!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)]。  
  
     [!code-csharp[System.Windows.Forms.Clipboard#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#2)]
     [!code-vb[System.Windows.Forms.Clipboard#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#2)]  
  
### <a name="to-retrieve-data-from-the-clipboard-in-a-custom-format"></a>若要从自定义格式在剪贴板中检索数据  
  
1.  使用<xref:System.Windows.Forms.Clipboard.GetData%2A>具有自定义格式名称的方法。 此方法是仅适用于[!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)]。  
  
     此外可以使用具有预定义的格式名称<xref:System.Windows.Forms.Clipboard.SetData%2A>方法。 有关详细信息，请参阅 <xref:System.Windows.Forms.DataFormats>。  
  
     [!code-csharp[System.Windows.Forms.Clipboard#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#3)]
     [!code-vb[System.Windows.Forms.Clipboard#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#3)]  
    [!code-csharp[System.Windows.Forms.Clipboard#100](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#100)]
    [!code-vb[System.Windows.Forms.Clipboard#100](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#100)]  
  
### <a name="to-retrieve-data-from-the-clipboard-in-multiple-formats"></a>若要从多个格式在剪贴板中检索数据  
  
1.  使用 <xref:System.Windows.Forms.Clipboard.GetDataObject%2A> 方法。 您必须使用此方法从版本在剪贴板中检索数据早于[!INCLUDE[dnprdnlong](../../../../includes/dnprdnlong-md.md)]。  
  
     [!code-csharp[System.Windows.Forms.Clipboard#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#4)]
     [!code-vb[System.Windows.Forms.Clipboard#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#4)]  
    [!code-csharp[System.Windows.Forms.Clipboard#100](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#100)]
    [!code-vb[System.Windows.Forms.Clipboard#100](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#100)]  
  
## <a name="see-also"></a>请参阅
- [拖放操作和剪贴板支持](drag-and-drop-operations-and-clipboard-support.md)
- [如何：将数据添加到剪贴板](how-to-add-data-to-the-clipboard.md)
