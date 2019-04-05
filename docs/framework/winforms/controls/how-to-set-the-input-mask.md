---
title: 如何：设置输入的掩码
ms.date: 03/30/2017
f1_keywords:
- net.ComponentModel.MaskPropertyEditor
helpviewer_keywords:
- MaskedTextBox control [Windows Forms]
ms.assetid: 779b3a12-cd74-4e58-b46e-04983bda5b2c
ms.openlocfilehash: 53bb8d0e301f83c25ab292b1cb6324dd5f21f100
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57702355"
---
# <a name="how-to-set-the-input-mask"></a>如何：设置输入的掩码
掩码的文本框控件是支持的声明性语法来接受或拒绝用户输入增强的文本框控件。 通过设置掩码属性，可以指定允许的用户输入，而无需在应用程序中编写任何自定义验证逻辑。 有关详细信息，请参阅备注部分的<xref:System.Windows.Forms.MaskedTextBox>类。  
  
## <a name="setting-the-mask-property-manually"></a>手动设置掩码属性  
 如果你熟悉使用掩码属性支持的字符，则可以手动输入它。 掩码属性支持的字符的摘要，请参阅备注部分的<xref:System.Windows.Forms.MaskedTextBox.Mask%2A>属性。  
  
#### <a name="to-set-the-mask-property-manually"></a>若要手动设置掩码属性  
  
1.  在中**设计**视图中，选择<xref:System.Windows.Forms.MaskedTextBox>。  
  
2.  在中**属性**窗口中，找到<xref:System.Windows.Forms.MaskedTextBox.Mask%2A>属性。  
  
3.  键入所需的掩码。 例如，键入 `###`。  
  
## <a name="using-the-input-mask-dialog-box"></a>使用输入的掩码对话框  
 输入掩码对话框中提供了一些预定义的输入的掩码。 此外可以更改的预定义的掩码或手动输入自己的掩码。  
  
#### <a name="to-open-the-input-mask-dialog-box"></a>若要打开输入掩码对话框  
  
1.  在中**设计**视图中，选择<xref:System.Windows.Forms.MaskedTextBox>。  
  
    1.  单击要打开的智能标记**MaskedTextBox 任务**面板。  
  
    2.  单击**设置掩码**。  
  
     \- 或 -  
  
    1.  在中**属性**窗口中，选择<xref:System.Windows.Forms.MaskedTextBox.Mask%2A>属性。  
  
    2.  单击属性值列中的省略号按钮。  
  
     **输入掩码**对话框随即出现。  
  
#### <a name="to-use-the-input-mask-dialog-box"></a>若要使用输入掩码对话框  
  
1.  （可选）单击其中一个列表中的预定义掩码。  
  
2.  （可选）编辑中的预定义的掩码**掩码**框。  
  
3.  （可选）输入新掩码**掩码**框。 也就是说，无需使用一个预定义的掩码。  
  
    > [!NOTE]
    >  预览框中会显示在用户将看到的字符<xref:System.Windows.Forms.MaskedTextBox>。 这些字符是指南可帮助用户正确输入数据。  
  
4.  选中或清除**使用 ValidatingType**复选框。 **使用 ValidatingType**复选框指定是否一种数据类型用于验证输入的数据由用户。 有关更多信息，请参见 <xref:System.Windows.Forms.MaskedTextBox.ValidatingType%2A> 属性。  
  
5.  单击 **“确定”**。  
  
     输入掩码**掩码**属性中的**属性**窗口。  
  
## <a name="see-also"></a>请参阅
- [演练：使用 MaskedTextBox 控件](walkthrough-working-with-the-maskedtextbox-control.md)
