---
title: 如何：将自定义区域添加到文件对话框
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Custom Place to dialog box
- adding Custom Place to dialog box
- CustomPlaces collection
ms.assetid: 63f6469b-59cd-40f6-9e61-8b5831856780
ms.openlocfilehash: d9c1373a16f7d62c2933e01e513478fc6c9866d2
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57721874"
---
# <a name="how-to-add-a-custom-place-to-a-file-dialog-box"></a>如何：将自定义区域添加到文件对话框
[!INCLUDE[wiprlhext](../../../../includes/wiprlhext-md.md)] 上的默认打开和保存对话框在名为“收藏夹链接”的对话框左侧有一个区域。 此区域称为自定义区域。 <xref:System.Windows.Forms.OpenFileDialog>并<xref:System.Windows.Forms.SaveFileDialog>类使您可以将文件夹添加到<xref:System.Windows.Forms.FileDialog.CustomPlaces%2A>集合。  
  
> [!NOTE]
>  为了使自定义可以出现在<xref:System.Windows.Forms.OpenFileDialog>或<xref:System.Windows.Forms.SaveFileDialog>，则<xref:System.Windows.Forms.FileDialog.AutoUpgradeEnabled%2A>属性必须设置为`true`（默认值）。  
  
### <a name="to-add-a-custom-place-to-a-file-dialog-box"></a>向文件对话框添加自定义区域  
  
-   添加路径，已知文件夹 GUID，或<xref:System.Windows.Forms.FileDialogCustomPlace>对象传递给<xref:System.Windows.Forms.FileDialog.CustomPlaces%2A>对话框中的集合。  
  
     以下代码示例演示了如何添加路径：  
  
    ```vb  
    OpenFileDialog1.CustomPlaces.Add("C:\MyCustomPlace")  
    ```  
  
    ```csharp  
    openFileDialog1.CustomPlaces.Add("C:\\MyCustomPlace");  
    ```  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.FileDialog>
- <xref:System.Windows.Forms.FileDialogCustomPlacesCollection.Add%2A?displayProperty=nameWithType>
- [文件对话框自定义区域的已知文件夹 GUID](known-folder-guids-for-file-dialog-custom-places.md)
