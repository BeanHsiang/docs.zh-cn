---
title: 各种自定义控件
ms.date: 03/30/2017
helpviewer_keywords:
- controls [Windows Forms], user controls
- controls [Windows Forms], types of
- composite controls [Windows Forms]
- extended controls [Windows Forms]
- controls [Windows Forms], extended
- user controls [Windows Forms]
- custom controls [Windows Forms]
- controls [Windows Forms], composite
ms.assetid: 3cea09e5-4344-4ccb-9858-b66ccac210ff
ms.openlocfilehash: 140b9284d9361aa149b4f739908376d1cbe6902c
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57713015"
---
# <a name="varieties-of-custom-controls"></a>各种自定义控件
使用 .NET Framework 可以开发和实现新的控件。 可以通过继承来扩展熟悉的用户控件和现有控件的功能。 还可以编写自定义控件，这些控件执行自己的绘制。  
  
 确定创建何种类型的控件可能令人困惑。 本主题重点介绍各种可继承控件之间的差异，并提供有关如何为项目选择某种特定控件的信息。  
  
> [!NOTE]
>  有关如何创作用于 Web 窗体的控件的信息，请参阅[开发自定义 ASP.NET 服务器控件](https://docs.microsoft.com/previous-versions/aspnet/zt27tfhy(v=vs.100))。  
  
## <a name="base-control-class"></a>基控件类  
 <xref:System.Windows.Forms.Control>类是 Windows 窗体控件的基类。 它提供了在 Windows 窗体应用程序中进行可视显示所需的基础结构。  
  
 <xref:System.Windows.Forms.Control>类执行以下任务以提供可在 Windows 窗体应用程序中的可视显示：  
  
-   公开窗口句柄。  
  
-   管理消息路由。  
  
-   提供鼠标和键盘事件，以及许多其他用户界面事件。  
  
-   提供高级布局功能。  
  
-   包含特定于可视显示许多属性，例如<xref:System.Windows.Forms.Control.ForeColor%2A>， <xref:System.Windows.Forms.Control.BackColor%2A>， <xref:System.Windows.Forms.Control.Height%2A>，和<xref:System.Windows.Forms.Control.Width%2A>。  
  
-   为 Windows 窗体控件充当 Microsoft® ActiveX® 控件提供必需的安全性和线程支持。  
  
 由于基类提供了大量基础结构，因此使开发自己的 Windows 窗体控件变得相对简单。  
  
## <a name="kinds-of-controls"></a>控件种类  
 Windows 窗体支持三种用户定义的控件：复合、扩展和自定义。 以下各节分别介绍各种控件，并就如何选择项目中使用的控件种类提供建议。  
  
### <a name="composite-controls"></a>复合控件  
 复合控件是封装在公共容器内的 Windows 窗体控件的集合。 这种控件有时称为用户控件。 其包含的控件称为构成控件。  
  
 复合控件包含与每个包含的 Windows 窗体控件相关联的所有固有功能，允许选择性地公开和绑定它们的属性。 复合控件还提供了大量的默认键盘处理功能，用户不需要进行任何额外的开发。  
  
 例如，可以生成复合控件，以显示来自数据库的客户地址数据。 此控件可包括<xref:System.Windows.Forms.DataGridView>控件来显示数据库字段中，<xref:System.Windows.Forms.BindingSource>来处理到数据源的绑定和一个<xref:System.Windows.Forms.BindingNavigator>控件以在记录之间移动。 可以选择性地公开数据绑定属性，还可以将整个控件打包并在不同应用程序之间重复使用。 这种复合控件的示例，请参阅[如何：应用 Windows 窗体控件中的特性](how-to-apply-attributes-in-windows-forms-controls.md)。  
  
 若要创作复合控件，派生<xref:System.Windows.Forms.UserControl>类。 <xref:System.Windows.Forms.UserControl>基类提供了键盘路由子控件，并使子控件作为组进行处理。 有关详细信息，请参阅[开发复合 Windows 窗体控件](developing-a-composite-windows-forms-control.md)。  
  
 **建议**  
  
 如果为以下情况，则从 <xref:System.Windows.Forms.UserControl> 类继承：  
  
-   你想要将多个 Windows 窗体控件的功能组合到单个可重用单元。  
  
### <a name="extended-controls"></a>扩展控件  
 你可以从任何现有的 Windows 窗体控件派生继承的控件。 使用此方法，你可以保留 Windows 窗体控件的所有固有功能，然后通过添加自定义属性、方法或其他功能来扩展该功能。 可以使用此选项重写基控件的绘制逻辑，然后通过更改该控件的外观来扩展其用户界面。  
  
 例如，可以创建一个派生自控件<xref:System.Windows.Forms.Button>控件，用于跟踪多少次用户单击它。  
  
 在某些控件中，您还可以自定义外观到您的控件的图形用户界面通过重写<xref:System.Windows.Forms.Control.OnPaint%2A>基类的方法。 对于跟踪单击次数的扩展按钮，您可以重写<xref:System.Windows.Forms.Control.OnPaint%2A>方法调用的基实现<xref:System.Windows.Forms.Control.OnPaint%2A>，然后的一角绘制单击计数<xref:System.Windows.Forms.Button>控件的客户端区域。  
  
 **建议**  
  
 如果为以下情况，则从 Windows 窗体控件继承：  
  
-   大部分所需功能与现有的 Windows 窗体控件相同。  
  
-   不需要自定义图形用户界面，或者想为现有控件设计一个新的图形用户界面。  
  
### <a name="custom-controls"></a>自定义控件  
 创建控件的另一种方法是创建继承，开始通过继承<xref:System.Windows.Forms.Control>。 <xref:System.Windows.Forms.Control>类提供了所有基本功能所需的控件，包括鼠标和键盘处理事件，但没有特定于控件的功能或图形界面。  
  
 通过继承创建控件<xref:System.Windows.Forms.Control>类需要更多的心思和精力相比从<xref:System.Windows.Forms.UserControl>或现有 Windows 窗体控件。 由于用户还需执行大量的实现，因此，控件可以具有比复合控件或扩展控件更好的灵活性，而且可以使控件完全满足自己的需要。  
  
 若要实现自定义控件，必须编写代码<xref:System.Windows.Forms.Control.OnPaint%2A>事件的控件，以及任何所需的特定于功能的代码。 此外可以重写<xref:System.Windows.Forms.Control.WndProc%2A>直接方法，并处理 windows 消息。 这是创建控件的最强大的方法，但若要有效地使用此技术，需熟悉 Microsoft Win32® API。  
  
 时钟控件即是一个自定义控件，它复制模拟时钟的外观和行为。 调用自定义绘制来使指针移动，以响应<xref:System.Windows.Forms.Timer.Tick>从内部事件<xref:System.Windows.Forms.Timer>组件。 有关详细信息，请参阅[如何：开发的简单 Windows 窗体控件](how-to-develop-a-simple-windows-forms-control.md)。  
  
 **建议**  
  
 如果为以下情况，则从 <xref:System.Windows.Forms.Control> 类继承：  
  
-   你想要提供控件的自定义图形表示形式。  
  
-   你需要实现不能通过标准控件实现的自定义功能。  
  
### <a name="activex-controls"></a>ActiveX 控件  
 尽管 Windows 窗体基础结构已为承载 Windows 窗体控件进行了优化，但仍可以使用 ActiveX 控件。 Visual Studio 中对此任务提供支持。 有关详细信息，请参阅[如何：向 Windows 窗体添加 ActiveX 控件](how-to-add-activex-controls-to-windows-forms.md)。  
  
### <a name="windowless-controls"></a>无窗口控件  
 Microsoft Visual Basic® 6.0 和 ActiveX 技术支持无窗口控件。 Windows 窗体中不支持无窗口控件。  
  
## <a name="custom-design-experience"></a>自定义设计体验  
 如果需要实现自定义设计时体验，可以创作自己的设计器。 对于复合控件类派生自定义设计器从<xref:System.Windows.Forms.Design.ParentControlDesigner>或<xref:System.Windows.Forms.Design.DocumentDesigner>类。 对于扩展和自定义控件类派生自定义设计器从<xref:System.Windows.Forms.Design.ControlDesigner>类。  
  
 使用<xref:System.ComponentModel.DesignerAttribute>以将控件与您的设计器相关联。 有关详细信息，请参阅[扩展设计时支持](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/37899azc(v=vs.120))和[如何：创建利用设计时功能的 Windows 窗体控件](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/307hck25(v=vs.120))。  
  
## <a name="see-also"></a>请参阅
- [使用 .NET Framework 开发自定义 Windows 窗体控件](developing-custom-windows-forms-controls.md)
- [如何：开发的简单 Windows 窗体控件](how-to-develop-a-simple-windows-forms-control.md)
- [开发复合 Windows 窗体控件](developing-a-composite-windows-forms-control.md)
- [扩展设计时支持](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/37899azc(v=vs.120))
- [如何：创建利用设计时功能的 Windows 窗体控件](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/307hck25(v=vs.120))
