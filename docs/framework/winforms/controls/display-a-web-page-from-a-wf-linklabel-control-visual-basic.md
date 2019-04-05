---
title: 如何：显示 Windows 窗体 LinkLabel 控件 (Visual Basic 中) 中的网页
ms.date: 03/30/2017
dev_langs:
- vb
f1_keywords:
- LinkLabel1_LinkClicked
helpviewer_keywords:
- examples [Windows Forms], LinkLabel control
- Web pages [Windows Forms], displaying
- linking [Windows Forms], to Web pages from forms
- Windows Forms, linking to Web pages
- LinkLabel control [Windows Forms], examples
ms.assetid: 477a7398-5971-4de3-b24c-f49f32bdb28a
ms.openlocfilehash: 7e80dba9cd43385be016506ac2a7e887a68dedf2
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57705222"
---
# <a name="how-to-display-a-web-page-from-a-windows-forms-linklabel-control-visual-basic"></a>如何：显示 Windows 窗体 LinkLabel 控件 (Visual Basic 中) 中的网页
此示例在默认浏览器中显示网页，当用户单击 Windows 窗体<xref:System.Windows.Forms.LinkLabel>控件。  
  
## <a name="example"></a>示例  
  
```vb  
Private Sub Form1_Load(ByVal sender As System.Object, ByVal e _  
As System.EventArgs) Handles MyBase.Load  
    LinkLabel1.Text = "Click here to get more info."  
    LinkLabel1.Links.Add(6, 4, "www.microsoft.com")  
End Sub  
Private Sub LinkLabel1_LinkClicked(ByVal sender As System.Object, ByVal _  
e As System.Windows.Forms.LinkLabelLinkClickedEventArgs) Handles _  
LinkLabel1.LinkClicked  
    System.Diagnostics.Process.Start(e.Link.LinkData.ToString())  
End Sub  
```  
  
## <a name="compiling-the-code"></a>编译代码  
 此示例需要：  
  
-   名为 Windows 窗体`Form1`。  
  
-   名为 `LinkLabel1` 的 <xref:System.Windows.Forms.LinkLabel> 控件。  
  
-   活动的 Internet 连接。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 对调用<xref:System.Diagnostics.Process.Start%2A>方法需要完全信任。 有关详细信息，请参阅 <xref:System.Security.SecurityException>。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.LinkLabel>
- [LinkLabel 控件](linklabel-control-windows-forms.md)
