---
title: 如何：显示 Web 样式链接使用 Windows 窗体 RichTextBox 控件
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- text boxes [Windows Forms], displaying Web links
- examples [Windows Forms], text boxes
- RichTextBox control [Windows Forms], linking to Web pages
ms.assetid: 95089a37-a202-4f7a-94ee-6ee312908851
ms.openlocfilehash: 64a2c8d9a9f6b8a7271a659b80ca2a63c423b3bc
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57718514"
---
# <a name="how-to-display-web-style-links-with-the-windows-forms-richtextbox-control"></a>如何：显示 Web 样式链接使用 Windows 窗体 RichTextBox 控件
Windows 窗体<xref:System.Windows.Forms.RichTextBox>控件可以显示为彩色并有下划线的 Web 链接。 可以编写将打开浏览器窗口中显示时单击该链接时链接文本中指定的 Web 站点的代码。  
  
### <a name="to-link-to-a-web-page-with-the-richtextbox-control"></a>若要链接到网页上使用 RichTextBox 控件  
  
1.  设置<xref:System.Windows.Forms.RichTextBox.Text%2A>属性设置为包含有效的 URL 的字符串 (例如，"http://www.microsoft.com/")。  
  
2.  请确保<xref:System.Windows.Forms.RichTextBox.DetectUrls%2A>属性设置为`true`（默认值）。  
  
3.  创建新的全局实例<xref:System.Diagnostics.Process>对象。  
  
4.  写入的事件处理程序<xref:System.Windows.Forms.RichTextBox.LinkClicked>发送所需的文本的浏览器的事件。  
  
     在以下示例中，<xref:System.Windows.Forms.RichTextBox.LinkClicked>事件将打开 Internet 浏览器中指定的 URL 来的实例<xref:System.Windows.Forms.RichTextBox.Text%2A>属性的<xref:System.Windows.Forms.RichTextBox>控件。 此示例假定窗体具有<xref:System.Windows.Forms.RichTextBox>控件。  
  
    > [!IMPORTANT]
    >  在调用<xref:System.Diagnostics.Process.Start%2A?displayProperty=nameWithType>方法，将会遇到<xref:System.Security.SecurityException>如果因特权不足而部分信任上下文中运行代码的异常。 有关详细信息，请参阅[代码访问安全性基础知识](../../misc/code-access-security-basics.md)。  
  
    ```vb  
    Public p As New System.Diagnostics.Process  
    Private Sub RichTextBox1_LinkClicked _  
       (ByVal sender As Object, ByVal e As _  
       System.Windows.Forms.LinkClickedEventArgs) _  
       Handles RichTextBox1.LinkClicked  
          ' Call Process.Start method to open a browser  
          ' with link text as URL.  
          p = System.Diagnostics.Process.Start("IExplore.exe", e.LinkText)  
    End Sub  
    ```  
  
    ```csharp  
    public System.Diagnostics.Process p = new System.Diagnostics.Process();  
  
    private void richTextBox1_LinkClicked(object sender,   
    System.Windows.Forms.LinkClickedEventArgs e)  
    {  
       // Call Process.Start method to open a browser  
       // with link text as URL.  
       p = System.Diagnostics.Process.Start("IExplore.exe", e.LinkText);  
    }  
    ```  
  
    ```cpp  
    public:  
       System::Diagnostics::Process ^ p;  
  
    private:  
       void richTextBox1_LinkClicked(System::Object ^  sender,  
          System::Windows::Forms::LinkClickedEventArgs ^  e)  
       {  
          // Call Process.Start method to open a browser  
          // with link text as URL.  
          p = System::Diagnostics::Process::Start("IExplore.exe",  
             e->LinkText);  
       }  
    ```  
  
     ([!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)])，则必须初始化过程`p`，您可以通过在你的窗体的构造函数中包含以下语句来执行此操作：  
  
    ```cpp  
    p = gcnew System::Diagnostics::Process();  
    ```  
  
     (Visual C#， [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]) 将以下代码放在窗体的构造函数，以注册事件处理程序。  
  
    ```csharp  
    this.richTextBox1.LinkClicked += new   
       System.Windows.Forms.LinkClickedEventHandler  
       (this.richTextBox1_LinkClicked);  
    ```  
  
    ```cpp  
    this->richTextBox1->LinkClicked += gcnew  
       System::Windows::Forms::LinkClickedEventHandler  
       (this, &Form1::richTextBox1_LinkClicked);  
    ```  
  
     请务必立即停止已创建完成后使用它的进程。 上面介绍的代码中引用，您的代码以停止该进程可能如下所示：  
  
    ```vb  
    Public Sub StopWebProcess()  
       p.Kill()  
    End Sub  
    ```  
  
    ```csharp  
    public void StopWebProcess()  
    {  
       p.Kill();  
    }  
    ```  
  
    ```cpp  
    public: void StopWebProcess()  
    {  
       p->Kill();  
    }  
    ```  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.RichTextBox.DetectUrls%2A>
- <xref:System.Windows.Forms.RichTextBox.LinkClicked>
- <xref:System.Windows.Forms.RichTextBox>
- [RichTextBox 控件](richtextbox-control-windows-forms.md)
- [在 Windows 窗体上使用的控件](controls-to-use-on-windows-forms.md)
