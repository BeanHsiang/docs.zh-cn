---
title: 演练：创建第一个触控应用程序
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- creating a touch-sensitive application [WPF]
- touchscreen applications [WPF], creating
- touch-sensitive applications [WPF], creating
- creating a touchscreen application [WPF]
ms.assetid: d69e602e-9a25-4e24-950b-e89eaa2a906b
ms.openlocfilehash: 2ebf22775ab9308bc896829be0b4e8cc147a3b4c
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57374149"
---
# <a name="walkthrough-creating-your-first-touch-application"></a>演练：创建第一个触控应用程序
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 使应用程序能够响应触摸。 例如，可以使用一个与应用程序交互或敏式设备，如本演练中创建该应用程序，用户可以移动，触摸屏上的多个手指重设大小，或使用触摸来旋转的单个对象。  
  
## <a name="prerequisites"></a>系统必备  
 你需要以下组件来完成本演练：  
  
-   Visual Studio。  
  
-   接受触控输入，如触摸屏，支持 Windows 触摸设备。  
  
 此外，应该基本了解如何创建中的应用程序的[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]，尤其是如何订阅和处理事件。 有关详细信息，请参见[演练：我第一个 WPF 桌面应用程序](../getting-started/walkthrough-my-first-wpf-desktop-application.md)。  
  
## <a name="creating-the-application"></a>创建应用程序  
  
#### <a name="to-create-the-application"></a>创建应用程序  
  
1.  在 Visual Basic 或 Visual C# 中创建名为 `BasicManipulation` 的新 WPF 应用程序项目。 有关详细信息，请参见[演练：我第一个 WPF 桌面应用程序](../getting-started/walkthrough-my-first-wpf-desktop-application.md)。  
  
2.  MainWindow.xaml 的内容替换为以下 XAML。  
  
     此标记将创建一个简单的应用程序包含一个红色<xref:System.Windows.Shapes.Rectangle>上<xref:System.Windows.Controls.Canvas>。 <xref:System.Windows.UIElement.IsManipulationEnabled%2A>属性的<xref:System.Windows.Shapes.Rectangle>设置为 true，以便它将接收操作事件。 应用程序订阅<xref:System.Windows.UIElement.ManipulationStarting>， <xref:System.Windows.UIElement.ManipulationDelta>，和<xref:System.Windows.UIElement.ManipulationInertiaStarting>事件。 这些事件包含的逻辑移动<xref:System.Windows.Shapes.Rectangle>用户处理。  
  
     [!code-xaml[BasicManipulation#UI](~/samples/snippets/csharp/VS_Snippets_Wpf/basicmanipulation/csharp/mainwindow.xaml#ui)]  
  
3.  如果使用的 Visual Basic 中，在 MainWindow.xaml 的第一行中，替换`x:Class="BasicManipulation.MainWindow"`与`x:Class="MainWindow"`。  
  
4.  在中`MainWindow`类中，添加以下<xref:System.Windows.UIElement.ManipulationStarting>事件处理程序。  
  
     <xref:System.Windows.UIElement.ManipulationStarting>事件发生时[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]检测到触控输入开始操作对象。 该代码指定操作位置应为相对于<xref:System.Windows.Window>通过设置<xref:System.Windows.Input.ManipulationStartingEventArgs.ManipulationContainer%2A>属性。  
  
     [!code-csharp[BasicManipulation#ManipulationStarting](~/samples/snippets/csharp/VS_Snippets_Wpf/basicmanipulation/csharp/mainwindow.xaml.cs#manipulationstarting)]
     [!code-vb[BasicManipulation#ManipulationStarting](~/samples/snippets/visualbasic/VS_Snippets_Wpf/basicmanipulation/visualbasic/mainwindow.xaml.vb#manipulationstarting)]

5.  在中`MainWindow`类中，添加以下<xref:System.Windows.Input.ManipulationDelta>事件处理程序。

     <xref:System.Windows.Input.ManipulationDelta>事件发生时触摸输入更改位置，并可在操作过程中出现多次。 引发一个手指后，也会发生该事件。 例如，如果用户在屏幕上拖动手指<xref:System.Windows.Input.ManipulationDelta>事件发生多次在手指移动时。 当用户将手指从屏幕上，<xref:System.Windows.Input.ManipulationDelta>事件会不断发生，以模拟惯性。

     此代码适用<xref:System.Windows.Input.ManipulationDeltaEventArgs.DeltaManipulation%2A>到<xref:System.Windows.UIElement.RenderTransform%2A>的<xref:System.Windows.Shapes.Rectangle>可将其移动用户在将移动触控输入。 它还会检查是否<xref:System.Windows.Shapes.Rectangle>的界限外<xref:System.Windows.Window>在惯性期间在事件发生时。 因此，在应用程序调用<xref:System.Windows.Input.ManipulationDeltaEventArgs.Complete%2A?displayProperty=nameWithType>方法来结束操作。

     [!code-csharp[BasicManipulation#ManipulationDelta](~/samples/snippets/csharp/VS_Snippets_Wpf/basicmanipulation/csharp/mainwindow.xaml.cs#manipulationdelta)]
     [!code-vb[BasicManipulation#ManipulationDelta](~/samples/snippets/visualbasic/VS_Snippets_Wpf/basicmanipulation/visualbasic/mainwindow.xaml.vb#manipulationdelta)]

6.  在中`MainWindow`类中，添加以下<xref:System.Windows.UIElement.ManipulationInertiaStarting>事件处理程序。

     <xref:System.Windows.UIElement.ManipulationInertiaStarting>事件发生时用户将所有手指从屏幕。 该代码设置初始速度和为移动、 扩展和旋转矩形的减速度。

     [!code-csharp[BasicManipulation#ManipulationInertiaStarting](~/samples/snippets/csharp/VS_Snippets_Wpf/basicmanipulation/csharp/mainwindow.xaml.cs#manipulationinertiastarting)]
     [!code-vb[BasicManipulation#ManipulationInertiaStarting](~/samples/snippets/visualbasic/VS_Snippets_Wpf/basicmanipulation/visualbasic/mainwindow.xaml.vb#manipulationinertiastarting)]

7.  生成并运行该项目。

     应会看到窗口中显示一个红色方块。

## <a name="testing-the-application"></a>测试应用程序
 若要测试应用程序，请尝试以下操作。 请注意，您可以多个以下项之一在同一时间。

-   若要将移动<xref:System.Windows.Shapes.Rectangle>，将手指放<xref:System.Windows.Shapes.Rectangle>并在屏幕上移动手指。

-   若要调整大小<xref:System.Windows.Shapes.Rectangle>，将两根手指放<xref:System.Windows.Shapes.Rectangle>，并将手指，或将其彼此相差。

-   若要旋转<xref:System.Windows.Shapes.Rectangle>，将两根手指放<xref:System.Windows.Shapes.Rectangle>和旋转相对于每个其他手指。

 若要导致延时，快速提升您将手指从屏幕执行上一操作。 <xref:System.Windows.Shapes.Rectangle>将继续移动、 调整大小，或为几秒钟才会停止旋转。

## <a name="see-also"></a>请参阅

- <xref:System.Windows.UIElement.ManipulationStarting?displayProperty=nameWithType>
- <xref:System.Windows.UIElement.ManipulationDelta?displayProperty=nameWithType>
- <xref:System.Windows.UIElement.ManipulationInertiaStarting?displayProperty=nameWithType>