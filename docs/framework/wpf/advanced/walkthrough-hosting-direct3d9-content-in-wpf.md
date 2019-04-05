---
title: 演练：在 WPF 中承载 Direct3D9 内容
ms.date: 03/30/2017
helpviewer_keywords:
- Direct3D9 [WPF interoperability], hosting Direct3D9 content
- WPF [WPF], hosting Direct3D9 content
ms.assetid: 60983736-0ab5-42cc-8b16-e9fbde261a43
ms.openlocfilehash: e588118e995694ea899b73d238e00f63e92feea4
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57352043"
---
# <a name="walkthrough-hosting-direct3d9-content-in-wpf"></a>演练：在 WPF 中承载 Direct3D9 内容
本演练演示如何承载 Windows Presentation Foundation (WPF) 应用程序中的 Direct3D9 内容。  
  
 在本演练中，你将要执行以下任务：  
  
-   创建用于承载 Direct3D9 内容的 WPF 项目。  
  
-   导入的 Direct3D9 内容。  
  
-   使用显示 Direct3D9 内容<xref:System.Windows.Interop.D3DImage>类。  
  
 完成后，您将知道如何进行承载 Direct3D9 内容在 WPF 应用程序。  
  
## <a name="prerequisites"></a>系统必备  
 你需要以下组件来完成本演练：  
  
-   Visual Studio。  
  
-   DirectX 9 或更高版本的 SDK。  
  
-   包含 WPF 兼容格式的 Direct3D9 内容的 DLL。 有关详细信息，请参阅[WPF 和 Direct3D9 互操作](wpf-and-direct3d9-interoperation.md)和[演练：创建在 WPF 中承载的 Direct3D9 内容](walkthrough-creating-direct3d9-content-for-hosting-in-wpf.md)。  
  
## <a name="creating-the-wpf-project"></a>创建 WPF 项目  
 第一步是创建 WPF 应用程序的项目。  
  
#### <a name="to-create-the-wpf-project"></a>创建 WPF 项目  
  
-   新的 WPF 应用程序项目中 Visual C# 创建名为`D3DHost`。 有关详细信息，请参见[演练：我第一个 WPF 桌面应用程序](../getting-started/walkthrough-my-first-wpf-desktop-application.md)。  
  
     在中打开 MainWindow.xaml [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)]。  
  
## <a name="importing-the-direct3d9-content"></a>导入的 Direct3D9 内容  
 使用导入的 Direct3D9 内容从非托管 DLL`DllImport`属性。  
  
#### <a name="to-import-direct3d9-content"></a>要导入 Direct3D9 内容  
  
1.  打开 MainWindow.xaml.cs 在代码编辑器中。  
  
2.  自动生成的代码替换为以下代码。  
  
     [!code-csharp[System.Windows.Interop.D3DImage#1](~/samples/snippets/csharp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/CS/window1.xaml.cs#1)]  
  
## <a name="hosting-the-direct3d9-content"></a>承载 Direct3D9 内容  
 最后，使用<xref:System.Windows.Interop.D3DImage>类以承载 Direct3D9 内容。  
  
#### <a name="to-host-the-direct3d9-content"></a>若要承载 Direct3D9 内容  
  
1.  在 MainWindow.xaml 中，自动生成的 XAML 将替换为以下 XAML。  
  
     [!code-xaml[System.Windows.Interop.D3DImage#10](~/samples/snippets/csharp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/CS/window1.xaml#10)]  
  
2.  生成项目。  
  
3.  将复制到 bin/Debug 文件夹的 Direct3D9 内容包含的 DLL。  
  
4.  按 F5 运行项目。  
  
     Direct3D9 内容出现在 WPF 应用程序。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Interop.D3DImage>
- [Direct3D9 和 WPF 互操作性的性能注意事项](performance-considerations-for-direct3d9-and-wpf-interoperability.md)
