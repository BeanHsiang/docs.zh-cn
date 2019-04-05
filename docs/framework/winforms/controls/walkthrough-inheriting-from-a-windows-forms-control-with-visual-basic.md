---
title: 演练：从使用 Visual Basic 的 Windows 窗体控件继承
ms.date: 03/30/2017
dev_langs:
- vb
helpviewer_keywords:
- inheritance [Windows Forms], custom controls
- inheritance [Windows Forms], control
- Windows Forms controls, inheritance
- inheritance [Windows Forms], walkthroughs
- custom controls [Windows Forms], inheritance
ms.assetid: fb58d7c8-b702-4478-ad31-b00cae118882
ms.openlocfilehash: 479e1a652c442651375c687288923f8abb60fd61
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57703486"
---
# <a name="walkthrough-inheriting-from-a-windows-forms-control-with-visual-basic"></a>演练：从使用 Visual Basic 的 Windows 窗体控件继承
使用 Visual Basic 中，可以创建功能强大的自定义控件，通过*继承*。 通过继承，可以创建不仅保留了标准 Windows 窗体控件的所有固有功能，而且还包含自定义功能的控件。 在本演练中，将创建一个名为 `ValueButton` 的简单继承控件。 此按钮将继承标准 Windows 窗体的功能<xref:System.Windows.Forms.Button>控件，并将公开一个名为的自定义属性`ButtonValue`。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
## <a name="creating-the-project"></a>创建项目  
 创建新的项目时应指定其名称，以设置根命名空间、程序集名称和项目名称，并确保默认组件将位于正确的命名空间中。  
  
#### <a name="to-create-the-valuebuttonlib-control-library-and-the-valuebutton-control"></a>创建 ValueButtonLib 控件库和 ValueButton 控件  
  
1.  在“文件”菜单上指向“新建”，然后单击“项目”打开“新建项目”对话框。  
  
2.  选择**Windows 窗体控件库**项目模板从列表中的 Visual Basic 项目，然后键入`ValueButtonLib`中**名称**框。  
  
     默认情况下，项目名称 `ValueButtonLib` 也会分配到根命名空间中。 根命名空间用于限定程序集中的组件名。 例如，如果两个程序集都提供名为 `ValueButton` 的组件，则可以使用 `ValueButtonLib.ValueButton` 指定 `ValueButton` 组件。 有关详细信息，请参阅 [Visual Basic 中的命名空间](~/docs/visual-basic/programming-guide/program-structure/namespaces.md)。  
  
3.  在“解决方案资源管理器”中，右键单击“UserControl1.vb”，然后从快捷菜单中选择“重命名”。 将文件名更改为 `ValueButton.vb`。 当系统询问是否重命名对代码元素“UserControl1”的所有引用时，单击“是”按钮。  
  
4.  在“解决方案资源管理器”中，单击“显示所有文件”按钮。  
  
5.  打开“ValueButton.vb”节点显示设计器生成的代码文件 **ValueButton.Designer.vb**。 在“代码编辑器”中打开此文件。  
  
6.  找到`Class`语句中， `Partial Public Class ValueButton`，并将该控件从从中要继承的类型更改<xref:System.Windows.Forms.UserControl>到<xref:System.Windows.Forms.Button>。 这允许继承的控件继承的所有功能<xref:System.Windows.Forms.Button>控件。  
  
7.  找到`InitializeComponent`方法，并删除的行，将分配<xref:System.Windows.Forms.ContainerControl.AutoScaleMode%2A>属性。 此属性中不存在<xref:System.Windows.Forms.Button>控件。  
  
8.  在“文件”菜单中，选择“全部保存”以保存项目。  
  
     请注意，可视化设计器不再可用。 因为<xref:System.Windows.Forms.Button>控件不自行绘制，则无法在设计器中修改其外观。 其可视表示形式将完全从它继承的类相同 (即， <xref:System.Windows.Forms.Button>) 除非在代码中修改。  
  
> [!NOTE]
>  但仍然可以向设计器图面添加不含 UI 元素的组件。  
  
## <a name="adding-a-property-to-your-inherited-control"></a>将属性添加到继承控件  
 继承的 Windows 窗体控件的可能用途之一是创建与标准 Windows 窗体控件的外观和行为相同、但公开自定义属性的控件。 在本节中，将向控件中添加名为 `ButtonValue` 的属性。  
  
#### <a name="to-add-the-value-property"></a>添加 Value 属性  
  
1.  在“解决方案资源管理器”中，右键单击“ValueButton.vb”，然后从快捷菜单中单击“查看代码”。  
  
2.  找到 `Public Class ValueButton` 语句。 在紧靠该语句下方键入以下代码：  
  
    ```vb  
    ' Creates the private variable that will store the value of your   
    ' property.  
    Private varValue as integer  
    ' Declares the property.  
    Property ButtonValue() as Integer  
    ' Sets the method for retrieving the value of your property.  
       Get  
          Return varValue  
       End Get  
    ' Sets the method for setting the value of your property.  
       Set(ByVal Value as Integer)  
          varValue = Value  
       End Set  
    End Property  
    ```  
  
     此代码设置存储和检索 `ButtonValue` 属性的方法。 `Get` 语句将返回的值设置为存储在私有变量 `varValue` 中的值，而 `Set` 语句通过使用 `Value` 关键字设置该私有变量的值。  
  
3.  在“文件”菜单中，选择“全部保存”以保存项目。  
  
## <a name="testing-your-control"></a>测试控件  
 控件不是独立的项目，它们必须托管在容器中。 若要测试控件，必须提供一个测试项目，以使控件在其中运行。 还必须通过生成（编译）该控件使测试项目能够访问它。 在本节中，将生成控件并在 Windows 窗体中对其进行测试。  
  
#### <a name="to-build-your-control"></a>生成控件  
  
1.  在 **“生成”** 菜单上，单击 **“生成解决方案”**。  
  
     生成应会成功，且没有任何编译器错误或警告。  
  
#### <a name="to-create-a-test-project"></a>创建测试项目  
  
1.  在“文件”菜单上，指向“添加”，然后单击“新建项目”打开“添加新项目”对话框。  
  
2.  选择 Visual Basic 项目节点，然后单击**Windows 窗体应用程序**。  
  
3.  在“名称”框中键入 `Test`。  
  
4.  在“解决方案资源管理器”中，单击“显示所有文件”按钮。  
  
5.  在“解决方案资源管理器”中，右键单击测试项目的“引用”节点，然后从快捷菜单上选择“添加引用”以显示“添加引用”对话框。  
  
6.  单击“项目”选项卡。  
  
7.  单击标记为“项目”的选项卡。 “项目名称”下将列出 `ValueButtonLib` 项目。 双击该项目将引用添加到测试项目。  
  
8.  在“解决方案资源管理器”中，右键单击“测试”，然后选择“生成”。  
  
#### <a name="to-add-your-control-to-the-form"></a>将控件添加到窗体  
  
1.  在“解决方案资源管理器”中，右键单击“Form1.vb”，然后从快捷菜单中选择“视图设计器”。  
  
2.  在“工具箱”中单击“ValueButtonLib 组件”。 双击“ValueButton”。  
  
     窗体上将出现“ValueButton”。  
  
3.  右键单击“ValueButton”，并从快捷菜单中选择“属性”。  
  
4.  在“属性”窗口中，检查该控件的属性。 请注意，除增加了一个 `ButtonValue` 属性外，它们与标准按钮公开的属性相同。  
  
5.  将 `ButtonValue` 属性设置为 `5`。  
  
6.  上**所有 Windows 窗体**选项卡**工具箱**，双击**标签**添加<xref:System.Windows.Forms.Label>向窗体控件。  
  
7.  将标签重新定位到窗体的中央。  
  
8.  双击 `ValueButton1`。  
  
     “代码编辑器”随即打开并显示 `ValueButton1_Click` 事件。  
  
9. 键入以下代码行。  
  
    ```vb  
    Label1.Text = CStr(ValueButton1.ButtonValue)  
    ```  
  
10. 在“解决方案资源管理器”中，右键单击“测试”，然后从快捷菜单中选择“设为启动项目”。  
  
11. 从“调试”菜单中选择“启动调试”。  
  
     `Form1` 将出现。  
  
12. 单击 `Valuebutton1`。  
  
     `Label1` 中显示数字“5”，表明继承的控件的 `ButtonValue` 属性已通过 `ValueButton1_Click` 方法传递给 `Label1`。 这样，`ValueButton` 控件便继承了标准 Windows 窗体按钮的所有功能，但是公开了一个附加的自定义属性。  
  
## <a name="see-also"></a>请参阅
- [演练：创作复合控件使用 Visual Basic](walkthrough-authoring-a-composite-control-with-visual-basic.md)
- [如何：中显示控件选择工具箱项对话框](how-to-display-a-control-in-the-choose-toolbox-items-dialog-box.md)
- [使用 .NET Framework 开发自定义 Windows 窗体控件](developing-custom-windows-forms-controls.md)
- [继承的基础知识 (Visual Basic)](~/docs/visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)
