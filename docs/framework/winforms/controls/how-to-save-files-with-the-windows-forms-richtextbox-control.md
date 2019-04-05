---
title: 如何：使用 Windows 窗体 RichTextBox 控件保存文件
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- saving files
- RTF files [Windows Forms], saving in RichTextBox control
- examples [Windows Forms], text boxes
- saving files [Windows Forms], RichTextBox control
- files [Windows Forms], saving with RichTextBox control
- RichTextBox control [Windows Forms], saving files
- .rtf files [Windows Forms], saving in RichTextBox control
- text files [Windows Forms], saving from RichTextBox control
ms.assetid: 4a58ec19-84d1-4383-9110-298c06adcfca
ms.openlocfilehash: c9a5d471a58c646c786cf441ee7d7ec235788f10
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57723018"
---
# <a name="how-to-save-files-with-the-windows-forms-richtextbox-control"></a>如何：使用 Windows 窗体 RichTextBox 控件保存文件
Windows 窗体<xref:System.Windows.Forms.RichTextBox>控件可以写入其显示在几种格式之一的信息：  
  
-   纯文本  
  
-   Unicode 纯文本  
  
-   丰富文本格式 (RTF)  
  
-   用空格代替 OLE 对象的 RTF  
  
-   使用 OLE 对象的文本表示形式的纯文本  
  
 若要保存文件，请调用<xref:System.Windows.Forms.RichTextBox.SaveFile%2A>方法。 此外可以使用**SaveFile**方法将数据保存到流。 有关详细信息，请参阅 <xref:System.Windows.Forms.RichTextBox.SaveFile%28System.IO.Stream%2CSystem.Windows.Forms.RichTextBoxStreamType%29>。  
  
### <a name="to-save-the-contents-of-the-control-to-a-file"></a>若要将控件的内容保存到文件  
  
1.  确定要保存的文件的路径。  
  
     若要执行此操作在实际应用程序中，通常可以使用<xref:System.Windows.Forms.SaveFileDialog>组件。 有关概述，请参阅[SaveFileDialog 组件概述](savefiledialog-component-overview-windows-forms.md)。  
  
2.  调用<xref:System.Windows.Forms.RichTextBox.SaveFile%2A>方法的<xref:System.Windows.Forms.RichTextBox>控件，指定要保存的文件和文件类型 （可选）。 如果调用使用文件名作为其唯一参数的方法，该文件将保存为 rtf 格式。 若要指定其他文件类型，请使用 <xref:System.Windows.Forms.RichTextBoxStreamType> 枚举的值作为其第二个参数来调用该方法。  
  
     在下面的示例中，将路径设置为格式文本文件的位置**我的文档**文件夹。 使用此位置是因为您可以假定大多数运行 Windows 操作系统的计算机将包含该文件夹。 选择此位置还允许具有最少的系统访问级别的用户安全地运行应用程序。 下面的示例假定窗体具有<xref:System.Windows.Forms.RichTextBox>已添加的控件。  
  
    ```vb  
    Public Sub SaveFile()  
       ' You should replace the bold file name in the   
       ' sample below with a file name of your own choosing.  
       RichTextBox1.SaveFile(System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       & "\Testdoc.rtf", _  
          RichTextBoxStreamType.RichNoOleObjs)  
    End Sub  
    ```  
  
    ```csharp  
    public void SaveFile()  
    {  
       // You should replace the bold file name in the   
       // sample below with a file name of your own choosing.  
       // Note the escape character used (@) when specifying the path.  
       richTextBox1.SaveFile(System.Environment.GetFolderPath  
       (System.Environment.SpecialFolder.Personal)  
       + @"\Testdoc.rtf",  
          RichTextBoxStreamType.RichNoOleObjs);  
    }  
    ```  
  
    ```cpp  
    public:  
       void SaveFile()  
       {  
          // You should replace the bold file name in the   
          // sample below with a file name of your own choosing.  
          richTextBox1->SaveFile(String::Concat  
             (System::Environment::GetFolderPath  
             (System::Environment::SpecialFolder::Personal),  
             "\\Testdoc.rtf"), RichTextBoxStreamType::RichNoOleObjs);  
       }  
    ```  
  
    > [!IMPORTANT]
    >  此示例在文件尚未存在时创建新文件。 如果应用程序需要创建一个文件，该应用程序将需要的文件夹创建访问权限。 可使用访问控制列表设置权限。 如果该文件已存在，该应用程序需要只写访问权限，较弱的特权。 在可能的情况下，会在部署期间，创建文件并仅授予对单个文件，读取访问权限而不是创建一个文件夹的访问更安全。 此外，较安全的做法是将数据写入用户文件夹，而不是根文件夹或“Program Files”文件夹。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.RichTextBox.SaveFile%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.RichTextBox>
- [RichTextBox 控件](richtextbox-control-windows-forms.md)
- [在 Windows 窗体上使用的控件](controls-to-use-on-windows-forms.md)
