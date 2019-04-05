---
title: 如何：创作复合控件
ms.date: 03/30/2017
helpviewer_keywords:
- UserControl class [Windows Forms], creating composite controls
- user controls [Windows Forms], creating
- user controls [Windows Forms], inheriting from
- composite controls [Windows Forms], creating
ms.assetid: 79c9cf05-5ab6-4a18-886d-88a64748b098
ms.openlocfilehash: cd82200706c98df18b1b9f464ebd62d797eea960
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57724448"
---
# <a name="how-to-author-composite-controls"></a>如何：创作复合控件
可通过多种方式使用复合控件。 可将其作为 Windows 桌面应用程序项目的一部分创作，并只在该项目的窗体上使用它们。 或者，可在 Windows 控件库项目中创作它们，将该项目编译为程序集，在其他项目中使用这些控件。 甚至可以从它们继承，并针对特殊目的使用视觉对象继承快速对它们进行自定义。  
  
> [!NOTE]
>  如果想要编写在 Web 窗体上使用的复合控件，请参阅[开发自定义 ASP.NET 服务器控件](https://docs.microsoft.com/previous-versions/aspnet/zt27tfhy(v=vs.100))。  
>   
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
### <a name="to-author-a-composite-control"></a>创作复合控件  
  
1.  打开一个名为 `DemoControlHost` 的新 **Windows 应用程序**项目。  
  
2.  在 **“项目”** 菜单上，单击 **“添加用户控件”**。  
  
3.  在“添加新项”对话框中，为类文件（.vb 或 .cs 文件）提供希望复合控件具有的名称。  
  
4.  选择**添加**按钮以创建复合控件的类文件。  
  
5.  将控件从“工具箱”添加到复合控件表面。  
  
6.  将代码置于事件过程中，处理由复合控件或其构成控件所引发的事件。  
  
7.  关闭复合控件的设计器，并在出现提示时保存文件。  
  
8.  在 **“生成”** 菜单上，单击 **“生成解决方案”**。  
  
     必须生成项目，自定义控件才可在“工具箱”中显示。  
  
9. 使用“工具箱”的“DemoControlHost”选项卡将控件的实例添加到 `Form1`。  
  
### <a name="to-author-a-control-class-library"></a>创作控件类库  
  
1.  打开新的“Windows 控件库”项目。  
  
     默认情况下，项目包含一个复合控件。  
  
2.  按照上述步骤中的说明添加控件和代码。  
  
3.  选择不想继承类更改的控件，并将此控件的“Modifiers”属性设置为“专用”。  
  
4.  生成 DLL。  
  
### <a name="to-inherit-from-a-composite-control-in-a-control-class-library"></a>从控件类库中的复合控件中继承  
  
1.  在“文件”菜单上，指向“添加”并选择“新建项目”，将新的“Windows 应用程序”项目添加到解决方案中。  
  
2.  在“解决方案资源管理器”中，右键单击新项目的“引用”文件夹，并选择“添加引用”以打开“添加引用”对话框。  
  
3.  选择“项目”选项卡，然后双击控件库项目。  
  
4.  在 **“生成”** 菜单上，单击 **“生成解决方案”**。  
  
5.  在“解决方案资源管理器”中，右键单击控件库项目并从快捷菜单中选择“添加新项”。  
  
6.  从“添加新项目”对话框中选择“继承的用户控件”模板。  
  
7.  在“继承选择器”对话框中，双击要继承的控件。  
  
     已将新控件添加到你的项目。  
  
8.  打开新控件的可视化设计器，并添加其他构成控件。  
  
     可看到从 DLL 中的复合控件继承的构成控件，还可以更改“Modifiers”属性为“Public”的控件的属性。 但不能更改“Modifiers”属性为“Private”的控件的属性。  
  
## <a name="see-also"></a>请参阅
- [演练：创作复合控件使用 Visual Basic](walkthrough-authoring-a-composite-control-with-visual-basic.md)
- [演练：创作复合控件通过视觉对象C#](walkthrough-authoring-a-composite-control-with-visual-csharp.md)
- [演练：从使用 Visual Basic 的 Windows 窗体控件继承](walkthrough-inheriting-from-a-windows-forms-control-with-visual-basic.md)
- [演练：从视觉对象的 Windows 窗体控件继承C#](walkthrough-inheriting-from-a-windows-forms-control-with-visual-csharp.md)
- [控件类型建议](control-type-recommendations.md)
- [如何：Windows 窗体的作者控件](how-to-author-controls-for-windows-forms.md)
- [各种自定义控件](varieties-of-custom-controls.md)
