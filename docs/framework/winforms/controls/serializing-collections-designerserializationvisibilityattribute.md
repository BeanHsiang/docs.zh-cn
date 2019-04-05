---
title: 演练：使用 DesignerSerializationVisibilityAttribute 序列化标准类型的集合
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- serialization [Windows Forms], collections
- standard types [Windows Forms], collections
- collections [Windows Forms], serializing
- collections [Windows Forms], standard types
ms.assetid: 020c9df4-fdc5-4dae-815a-963ecae5668c
ms.openlocfilehash: b5b5295e61f2a417c3565e62000021019381536f
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57712183"
---
# <a name="walkthrough-serializing-collections-of-standard-types-with-the-designerserializationvisibilityattribute"></a>演练：使用 DesignerSerializationVisibilityAttribute 序列化标准类型的集合
自定义控件有时将公开为属性的集合。 本演练演示如何使用<xref:System.ComponentModel.DesignerSerializationVisibilityAttribute>类来控制在设计时序列化集合的方式。 将应用<xref:System.ComponentModel.DesignerSerializationVisibilityAttribute.Content>到集合属性的值可确保将序列化属性。  
  
 要将本主题中的代码作为单个列表进行复制，请参阅[如何：序列化使用 DesignerSerializationVisibilityAttribute 标准类型的集合](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/ms171833(v=vs.120))。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
## <a name="prerequisites"></a>系统必备  
 若要完成本演练，你将需要：  
  
-   若要能够创建和安装 Visual Studio 的计算机上运行 Windows 窗体应用程序项目的足够权限。  
  
## <a name="creating-a-control-that-has-a-serializable-collection"></a>创建一个控件具有可序列化集合  
 第一步是创建具有可序列化集合作为属性的控件。 您可以编辑此集合使用的内容**集合编辑器**，使用户能够从**属性**窗口。  
  
#### <a name="to-create-a-control-with-a-serializable-collection"></a>若要创建具有可序列化集合的控件  
  
1.  创建一个名为 Windows 控件库项目`SerializationDemoControlLib`。 有关详细信息，请参阅[Windows 控件库模板](https://docs.microsoft.com/previous-versions/kxczf775(v=vs.100))。  
  
2.  重命名`UserControl1`到`SerializationDemoControl`。 有关详细信息，请参阅[重命名代码符号重构](/visualstudio/ide/reference/rename)。  
  
3.  在中**属性**窗口中，设置的值<xref:System.Windows.Forms.Padding.All%2A?displayProperty=nameWithType>属性设置为`10`。  
  
4.  位置<xref:System.Windows.Forms.TextBox>控件中`SerializationDemoControl`。  
  
5.  选择 <xref:System.Windows.Forms.TextBox> 控件。 在中**属性**窗口中，设置以下属性。  
  
    |属性|更改为|  
    |--------------|---------------|  
    |**多行**|`true`|  
    |**Dock**|<xref:System.Windows.Forms.DockStyle.Fill>|  
    |**ScrollBars**|<xref:System.Windows.Forms.ScrollBars.Vertical>|  
    |**ReadOnly**|`true`|  
  
6.  在中**代码编辑器**，声明一个名为的字符串数组字段`stringsValue`中`SerializationDemoControl`。  
  
     [!code-cpp[System.ComponentModel.DesignerSerializationVisibilityAttribute#4](~/samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/cpp/form1.cpp#4)]
     [!code-csharp[System.ComponentModel.DesignerSerializationVisibilityAttribute#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/CS/form1.cs#4)]
     [!code-vb[System.ComponentModel.DesignerSerializationVisibilityAttribute#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/VB/form1.vb#4)]  
  
7.  定义`Strings`属性上的`SerializationDemoControl`。  
  
> [!NOTE]
>  <xref:System.ComponentModel.DesignerSerializationVisibilityAttribute.Content>值用于启用序列化的集合。  
  
 [!code-cpp[System.ComponentModel.DesignerSerializationVisibilityAttribute#5](~/samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/cpp/form1.cpp#5)]
 [!code-csharp[System.ComponentModel.DesignerSerializationVisibilityAttribute#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/CS/form1.cs#5)]
 [!code-vb[System.ComponentModel.DesignerSerializationVisibilityAttribute#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/VB/form1.vb#5)]  
  
1.  按 F5 生成项目并在“UserControl 测试容器”中运行该控件。  
  
2.  查找`Strings`中的属性<xref:System.Windows.Forms.PropertyGrid>的**UserControl 测试容器**。 单击`Strings`属性，然后单击省略号 (![VisualStudioEllipsesButton 屏幕快照](../media/vbellipsesbutton.png "vbEllipsesButton")) 按钮以打开**字符串集合编辑器**.  
  
3.  输入中的多个字符串**字符串集合编辑器**。 分隔通过按每个字符串的末尾处的 ENTER 键。 单击**确定**完后输入字符串。  
  
> [!NOTE]
>  您键入的字符串出现在<xref:System.Windows.Forms.TextBox>的`SerializationDemoControl`。  
  
## <a name="serializing-a-collection-property"></a>序列化集合属性  
 若要测试您的控件的序列化行为，会将其放在窗体上并更改与集合中的内容**集合编辑器**。 可以通过查看特殊的设计器文件，在其中看到序列化的集合状态**Windows 窗体设计器**发出的代码。  
  
#### <a name="to-serialize-a-collection"></a>序列化集合  
  
1.  向解决方案添加一个 Windows 应用程序项目。 将项目命名为 `SerializationDemoControlTest`。  
  
2.  在中**工具箱**，找到名为选项卡**SerializationDemoControlLib 组件**。 在此选项卡上，您会发现`SerializationDemoControl`。 有关详细信息，请参见[演练：自动填充工具箱与自定义组件](walkthrough-automatically-populating-the-toolbox-with-custom-components.md)。  
  
3.  位置`SerializationDemoControl`窗体上。  
  
4.  查找`Strings`中的属性**属性**窗口。 单击`Strings`属性，然后单击省略号 (![VisualStudioEllipsesButton 屏幕快照](../media/vbellipsesbutton.png "vbEllipsesButton")) 按钮以打开**字符串集合编辑器**.  
  
5.  键入在多个字符串**字符串集合编辑器**。 分隔通过按每个字符串的末尾处的 ENTER 键。 单击**确定**完后输入字符串。  
  
> [!NOTE]
>  您键入的字符串出现在<xref:System.Windows.Forms.TextBox>的`SerializationDemoControl`。  
  
1.  在“解决方案资源管理器”中，单击“显示所有文件”按钮。  
  
2.  打开**Form1**节点。 它是名为的文件下**Form1.Designer.cs**或**Form1.Designer.vb**。 这是在其中的文件**Windows 窗体设计器**发出代码，表示窗体及其子控件的设计时状态。 在“代码编辑器”中打开此文件。  
  
3.  打开名为的区域**Windows 窗体设计器生成的代码**并找到标记为部分**serializationDemoControl1**。 在此标签下是表示控件的序列化的状态的代码。 键入在步骤 5 中的字符串出现在赋值`Strings`属性。 C# 和 Visual Basic 中的以下代码示例显示的代码类似于您将看到的内容键入字符串"red"、"橙色"和"黄色"。  
  
    ```csharp  
    this.serializationDemoControl1.Strings = new string[] {  
            "red",  
            "orange",  
            "yellow"};  
    ```  
    
    ```vb  
    Me.serializationDemoControl1.Strings = New String() {"red", "orange", "yellow"}  
    ```
  
4.  在中**代码编辑器**，更改的值<xref:System.ComponentModel.DesignerSerializationVisibilityAttribute>上`Strings`属性设置为<xref:System.ComponentModel.DesignerSerializationVisibility.Hidden>。  
  
    ```csharp  
    [DesignerSerializationVisibility(DesignerSerializationVisibility.Hidden)]  
    ```  
    ```vb  
    <DesignerSerializationVisibility(DesignerSerializationVisibility.Hidden)> _  
    ```  
  
5. 重新生成解决方案和重复执行步骤 3 和 4。  
  
> [!NOTE]
>  在这种情况下， **Windows 窗体设计器**发出分配给`Strings`属性。  
  
## <a name="next-steps"></a>后续步骤  
 一旦您知道如何进行序列化标准类型的集合，请考虑将你的自定义控件更深入地集成到设计时环境。 以下主题介绍如何增强你的自定义控件的设计时集成：  
  
-   [设计时体系结构](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/c5z9s1h4(v=vs.120))  
  
-   [Windows 窗体控件中的特性](attributes-in-windows-forms-controls.md)  
  
-   [设计器序列化概述](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/ms171834(v=vs.120))  
  
-   [演练：创建利用 Visual Studio 设计时功能的 Windows 窗体控件](creating-a-wf-control-design-time-features.md)  
  
## <a name="see-also"></a>请参阅
- <xref:System.ComponentModel.DesignerSerializationVisibilityAttribute>
- [设计器序列化概述](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/ms171834(v=vs.120))
- [如何：序列化使用 DesignerSerializationVisibilityAttribute 标准类型的集合](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/ms171833(v=vs.120))
- [演练：自动填充工具箱与自定义组件](walkthrough-automatically-populating-the-toolbox-with-custom-components.md)
