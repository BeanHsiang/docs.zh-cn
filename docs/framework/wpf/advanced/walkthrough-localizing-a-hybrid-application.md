---
title: 演练：本地化混合应用程序
ms.date: 08/18/2018
helpviewer_keywords:
- localization [WPF interoperability]
- hybrid applications [WPF interoperability]
ms.assetid: fbc0c54e-930a-4c13-8e9c-27b83665010a
ms.openlocfilehash: 116a847d4f7b0591e823416cf5744e68d689c6ee
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57378075"
---
# <a name="walkthrough-localizing-a-hybrid-application"></a>演练：本地化混合应用程序

本演练演示如何将本地化[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]中的元素[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]-基于混合应用程序。

本演练涉及以下任务：

-   创建[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]宿主项目。

-   添加可本地化的内容。

-   启用本地化。

-   分配资源标识符。

-   使用 LocBaml 工具生成附属程序集。

在本演练中所涉及任务的完整代码列表，请参阅[本地化混合应用程序示例](https://go.microsoft.com/fwlink/?LinkID=160015)。

完成后，你将拥有一个本地化的混合应用程序。

## <a name="prerequisites"></a>系统必备

你需要以下组件来完成本演练：

-   Visual Studio 2017

## <a name="creating-the-windows-forms-host-project"></a>创建 Windows 窗体宿主项目

第一步是创建[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]应用程序项目，并添加[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]包含要本地化的内容元素。

### <a name="to-create-the-host-project"></a>创建宿主项目

1.  创建**WPF 应用程序**名为项目`LocalizingWpfInWf`。  (**文件** > **新** > **项目** > **Visual C#** 或**Visual Basic**  > **经典桌面** > **WPF 应用程序**)。

2.  添加[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]<xref:System.Windows.Controls.UserControl>元素称为`SimpleControl`到项目。

3.  使用<xref:System.Windows.Forms.Integration.ElementHost>控件中放置`SimpleControl`窗体上的元素。 有关详细信息，请参见[演练：承载 3-D WPF 复合控件在 Windows 窗体中的](walkthrough-hosting-a-3-d-wpf-composite-control-in-windows-forms.md)。

## <a name="adding-localizable-content"></a>添加可本地化的内容

接下来，您将添加[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]标签控件，并设置[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]到可本地化的字符串的元素的内容。

### <a name="to-add-localizable-content"></a>添加可本地化的内容

1.  在中**解决方案资源管理器**，双击**SimpleControl.xaml**中打开[!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)]。

2.  设置的内容<xref:System.Windows.Controls.Button>控制是通过使用下面的代码。

     [!code-xaml[LocalizingWpfInWf#10](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizingWpfInWf/CSharp/SimpleControl0.xaml#10)]

3.  在中**解决方案资源管理器**，双击**Form1**若要在 Windows 窗体设计器中打开它。

4.  打开**工具箱**，然后双击**标签**标签控件添加到窗体。 将其 <xref:System.Windows.Forms.Control.Text%2A> 属性的值设置为 `"Hello"`。

5.  按 F5 生成并运行该应用程序。

     这两个`SimpleControl`元素和标签控件显示文本 **"Hello"**。

## <a name="enabling-localization"></a>启用本地化

Windows 窗体设计器提供用于在附属程序集中启用本地化的设置。

### <a name="to-enable-localization"></a>启用本地化

1.  在中**解决方案资源管理器**，双击**Form1.cs**若要在 Windows 窗体设计器中打开它。

2.  在中**属性**窗口中，将窗体的值**Localizable**属性设置为`true`。

3.  在中**属性**窗口中，设置的值**语言**属性设置为**西班牙语 （西班牙）**。

4.  在 Windows 窗体设计器中，选择标签控件。

5.  在中**属性**窗口中，设置的值<xref:System.Windows.Forms.Control.Text%2A>属性设置为`"Hola"`。

     一个名为 Form1.es-ES.resx 的新资源文件会添加到项目中。

6.  在中**解决方案资源管理器**，右键单击**Form1.cs**然后单击**查看代码**以在代码编辑器中打开它。

7.  以下代码复制到`Form1`构造函数，然后调用`InitializeComponent`。

     [!code-csharp[LocalizingWpfInWf#2](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizingWpfInWf/CSharp/Form1.cs#2)]

8.  在中**解决方案资源管理器**，右键单击**LocalizingWpfInWf**然后单击**卸载项目**。

     项目名称将标记为 **（不可用）**。

9. 右键单击**LocalizingWpfInWf**，然后单击**编辑 LocalizingWpfInWf.csproj**。

     项目文件将在代码编辑器中打开。

10. 将以下行复制到第一个`PropertyGroup`项目文件中。

    ```xml
    <UICulture>en-US</UICulture>
    ```

11. 保存项目文件并将其关闭。

12. 在中**解决方案资源管理器**，右键单击**LocalizingWpfInWf**然后单击**重新加载项目**。

## <a name="assigning-resource-identifiers"></a>分配资源标识符

可以通过使用资源标识符将可本地化内容映射到资源程序集。 MsBuild.exe 应用程序会自动分配资源标识符，当您指定`updateuid`选项。

### <a name="to-assign-resource-identifiers"></a>分配资源标识符

1.  从开始菜单中，打开 Visual Studio 开发人员命令提示。

2.  使用以下命令将资源标识符分配到可本地化内容。

    ```
    msbuild -t:updateuid LocalizingWpfInWf.csproj
    ```

3.  在中**解决方案资源管理器**，双击**SimpleControl.xaml**以在代码编辑器中打开它。 你将看到`msbuild`命令添加`Uid`所有元素的都属性。 这有助于通过分配资源标识符进行本地化。

     [!code-xaml[LocalizingWpfInWf#20](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizingWpfInWf/CSharp/SimpleControl.xaml#20)]

4.  按**F6**以生成解决方案。

## <a name="using-locbaml-to-produce-a-satellite-assembly"></a>使用 LocBaml 生成附属程序集

本地化的内容存储在纯资源*附属程序集*。 使用命令行工具 LocBaml.exe 生成本地化程序集为你[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]内容。

### <a name="to-produce-a-satellite-assembly"></a>生成附属程序集

1.  将 LocBaml.exe 复制到项目的 obj\Debug 文件夹中。 有关详细信息，请参阅[本地化应用程序](how-to-localize-an-application.md)。

2.  在“命令提示符”窗口中，使用以下命令将资源字符串提取到临时文件中。

    ```
    LocBaml /parse LocalizingWpfInWf.g.en-US.resources /out:temp.csv
    ```

3.  使用 Visual Studio 或其他文本编辑器打开 temp.csv 文件。 字符串替换为`"Hello"`使用其西班牙语翻译`"Hola"`。

4.  保存 temp.csv 文件。

5.  使用以下命令生成本地化资源文件。

    ```
    LocBaml /generate /trans:temp.csv LocalizingWpfInWf.g.en-US.resources /out:. /cul:es-ES
    ```

     将在 obj\Debug 文件夹中创建 LocalizingWpfInWf.g.es-ES.resources 文件。

6.  使用以下命令生成本地化附属程序集。

    ```
    Al.exe /out:LocalizingWpfInWf.resources.dll /culture:es-ES /embed:LocalizingWpfInWf.Form1.es-ES.resources /embed:LocalizingWpfInWf.g.es-ES.resources
    ```

     将在 obj\Debug 文件夹中创建 LocalizingWpfInWf.resources.dll 文件。

7.  将 LocalizingWpfInWf.resources.dll 文件复制到项目的 bin\Debug\es-ES 文件夹中。 替换现有文件。

8.  运行 LocalizingWpfInWf.exe，它位于项目的 bin\Debug 文件夹中。 不要重新生成应用程序，否则附属程序集将被覆盖。

     应用程序显示本地化后的字符串，而不是英语字符串。

## <a name="see-also"></a>请参阅

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [对应用程序进行本地化](how-to-localize-an-application.md)
- [演练：本地化 Windows 窗体](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/y99d1cd3(v=vs.100))
- [在 Visual Studio 中设计 XAML](/visualstudio/designers/designing-xaml-in-visual-studio)
