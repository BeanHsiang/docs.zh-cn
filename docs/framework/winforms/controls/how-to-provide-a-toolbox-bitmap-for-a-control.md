---
title: 如何：为控件提供工具箱位图
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Toolbox [Windows Forms], adding bitmaps for custom controls
- custom controls [Windows Forms], Toolbox bitmaps
- bitmaps [Windows Forms], custom controls
ms.assetid: 0ed0840a-616d-41ba-a27d-3573241932ad
ms.openlocfilehash: 9072f96bd6e3485e759ed72819229b3f0c33d641
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57715953"
---
# <a name="how-to-provide-a-toolbox-bitmap-for-a-control"></a>如何：为控件提供工具箱位图
如果你想要有一个特殊的图标为您的控件出现在**工具箱**，可以通过使用指定的特定映像<xref:System.Drawing.ToolboxBitmapAttribute>。 此类是一个特性，是一种可以附加到其他类上的特殊类。 有关属性的详细信息，请参阅[(Visual Basic 中) 的特性概述](../../../visual-basic/programming-guide/concepts/attributes/index.md)适用于 Visual Basic 或[特性 (C#)](../../../csharp/programming-guide/concepts/attributes/index.md)适用于 C#。  
  
 使用<xref:System.Drawing.ToolboxBitmapAttribute>，可以指定一个字符串，指示一个 16 × 16 像素的位图的路径和文件名称。 添加到“工具箱”后，此位图显示在对应的控件旁边。 此外可以指定<xref:System.Type>，在这种情况下加载与该类型关联的位图。 如果同时指定<xref:System.Type>字符串，该控件中搜索的图像资源中包含由指定的类型的程序集的字符串参数所指定的名称和<xref:System.Type>参数。  
  
### <a name="to-specify-a-toolbox-bitmap-for-your-control"></a>指定控件的工具箱位图  
  
1.  添加<xref:System.Drawing.ToolboxBitmapAttribute>到类声明之前控件的`Class`对于 visual Basic，及更高版本的类声明对于 Visual C# 关键字。  
  
    ```vb  
    ' Specifies the bitmap associated with the Button type.  
    <ToolboxBitmap(GetType(Button))> Class MyControl1  
    ' Specifies a bitmap file.  
    End Class  
    <ToolboxBitmap("C:\Documents and Settings\Joe\MyPics\myImage.bmp")> _  
       Class MyControl2  
    End Class  
    ' Specifies a type that indicates the assembly to search, and the name   
    ' of an image resource to look for.  
    <ToolboxBitmap(GetType(MyControl), "MyControlBitmap")> Class MyControl  
    End Class  
    ```  
  
    ```csharp  
    // Specifies the bitmap associated with the Button type.  
    [ToolboxBitmap(typeof(Button))]  
    class MyControl1 : UserControl  
    {  
    }  
    // Specifies a bitmap file.  
    [ToolboxBitmap(@"C:\Documents and Settings\Joe\MyPics\myImage.bmp")]  
    class MyControl2 : UserControl  
    {  
    }  
    // Specifies a type that indicates the assembly to search, and the name   
    // of an image resource to look for.  
    [ToolboxBitmap(typeof(MyControl), "MyControlBitmap")]  
    class MyControl : UserControl  
    {  
    }  
    ```  
  
2.  重新生成项目。  
  
    > [!NOTE]
    >  对于自动生成的控件和组件，位图不会出现在工具箱中。 若要查看位图，请使用“选择工具箱项”对话框重载控件。 有关详细信息，请参见[演练：自动填充工具箱与自定义组件](walkthrough-automatically-populating-the-toolbox-with-custom-components.md)。  
  
## <a name="see-also"></a>请参阅

- <xref:System.Drawing.ToolboxBitmapAttribute>
- [演练：自动填充工具箱与自定义组件](walkthrough-automatically-populating-the-toolbox-with-custom-components.md)
- [设计时开发 Windows 窗体控件](developing-windows-forms-controls-at-design-time.md)
- [特性概述 (Visual Basic)](../../../visual-basic/programming-guide/concepts/attributes/index.md)
- [特性 (C#)](../../../csharp/programming-guide/concepts/attributes/index.md)
