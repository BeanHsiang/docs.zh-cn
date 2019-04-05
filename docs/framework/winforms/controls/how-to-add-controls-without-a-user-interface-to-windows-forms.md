---
title: 如何：向 Windows 窗体添加无用户界面控件
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
f1_keywords:
- NonVisualSelection
helpviewer_keywords:
- invisible controls [Windows Forms]
- Windows Forms controls, adding to form
- controls [Windows Forms], nonvisual
- Windows Forms controls, nonvisual
- nonvisual controls [Windows Forms]
ms.assetid: 52134d9c-cff6-4eed-8e2b-3d5eb3bd494e
ms.openlocfilehash: 4d99f56710fa1d879aed5000edb5424a0727ae3c
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57703619"
---
# <a name="how-to-add-controls-without-a-user-interface-to-windows-forms"></a>如何：向 Windows 窗体添加无用户界面控件
非可视控件 （或组件） 提供了与你的应用程序的功能。 不同于其他控件组件不向用户提供用户界面，因此不需要在 Windows 窗体设计器图面上显示。 当一个组件添加到窗体时，Windows 窗体设计器在其中显示所有组件的窗体的底部显示可调整大小的送纸器。 控件添加到组件栏后，你可以选择的组件，并设置其属性，就像任何其他控件在窗体上。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
### <a name="to-add-a-component-to-a-windows-form"></a>若要将组件添加到 Windows 窗体  
  
1.  打开窗体。 有关详细信息，请参阅[如何：在设计器中显示 Windows 窗体](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/w5yd62ts(v=vs.100))。  
  
2.  在中**工具箱**，单击一个组件，并将其拖动到窗体。  
  
     此组件将出现在组件栏中。  
  
 此外，组件可以在运行时添加到窗体中。 这是一种常见方案，特别是因为组件不具有直观的表达与具有用户界面的控件不同。 在以下示例中，<xref:System.Windows.Forms.Timer>在运行时添加组件。 (请注意，Visual Studio 包含多种不同的计时器; 在这种情况下，使用 Windows 窗体<xref:System.Windows.Forms.Timer>组件。 有关在 Visual Studio 中不同的计时器的详细信息，请参阅[基于服务器的计时器简介](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/tb9yt5e6(v=vs.90))。)  
  
> [!CAUTION]
>  组件通常具有必须为有效运行该组件设置的特定于控件的属性。 情况下<xref:System.Windows.Forms.Timer>下方的组件，您将设置`Interval`属性。 请确保，在将组件添加到项目中，您设置属性，该组件必需的。  
  
#### <a name="to-add-a-component-to-a-windows-form-programmatically"></a>若要以编程方式向 Windows 窗体添加组件  
  
1.  创建的实例<xref:System.Windows.Forms.Timer>代码中的类。  
  
2.  设置`Interval`属性，以确定计时器的滴答之间的时间。  
  
3.  配置任何其他必要的属性，为您的组件。  
  
     下面的代码演示如何创建<xref:System.Windows.Forms.Timer>使用其`Interval`属性集。  
  
    ```vb  
    Public Sub CreateTimer()  
       Dim timerKeepTrack As New System.Windows.Forms.Timer  
       timerKeepTrack.Interval = 1000  
    End Sub  
    ```  
  
    ```csharp  
    public void createTimer()  
    {  
       System.Windows.Forms.Timer timerKeepTrack = new  
           System.Windows.Forms.Timer();  
       timerKeepTrack.Interval = 1000;  
    }  
    ```  
  
    ```cpp  
    public:  
       void createTimer()  
       {  
          System::Windows::Forms::Timer^ timerKeepTrack = gcnew  
             System::Windows::Forms::Timer();  
          timerKeepTrack->Interval = 1000;  
       }  
    ```  
  
    > [!IMPORTANT]
    >  通过引用恶意 UserControl，可能会使您的本地计算机通过网络安全风险。 这只能在恶意的用户创建一个具有破坏性的自定义控件，跟您错误地将其添加到你的项目的情况下一个问题。  
  
## <a name="see-also"></a>请参阅
- [Windows 窗体控件](index.md)
- [如何：向 Windows 窗体添加控件](how-to-add-controls-to-windows-forms.md)
- [如何：向 Windows 窗体添加 ActiveX 控件](how-to-add-activex-controls-to-windows-forms.md)
- [如何：Windows 窗体之间复制控件](how-to-copy-controls-between-windows-forms.md)
- [将控件置于 Windows 窗体上](putting-controls-on-windows-forms.md)
- [标记各个 Windows 窗体控件并创建它们的快捷键](labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)
- [在 Windows 窗体上使用的控件](controls-to-use-on-windows-forms.md)
- [按功能列出的 Windows 窗体控件](windows-forms-controls-by-function.md)
