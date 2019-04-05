---
title: 演练：创建在 WPF 中承载的 Direct3D9 内容
ms.date: 03/30/2017
dev_langs:
- cpp
helpviewer_keywords:
- WPF [WPF], creating Direct3D9 content
- Direct3D9 [WPF interoperability], creating Direct3D9 content
ms.assetid: 286e98bc-1eaa-4b5e-923d-3490a9cca5fc
ms.openlocfilehash: 8acef4a52c9317618485a7c46c1e22cc2524dd69
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57379596"
---
# <a name="walkthrough-creating-direct3d9-content-for-hosting-in-wpf"></a>演练：创建在 WPF 中承载的 Direct3D9 内容
本演练演示如何创建适用于 Windows Presentation Foundation (WPF) 应用程序中承载的 Direct3D9 内容。 承载 WPF 应用程序中的 Direct3D9 内容的详细信息，请参阅[WPF 和 Direct3D9 互操作](wpf-and-direct3d9-interoperation.md)。

 在本演练中，你将要执行以下任务：

-   创建 Direct3D9 项目。

-   配置用于 WPF 应用程序中承载的 Direct3D9 项目。

 完成，你将拥有一个 DLL，它包含在 WPF 应用程序中使用的 Direct3D9 内容。

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

-   Visual Studio 2010。

-   DirectX 9 或更高版本的 SDK。

## <a name="creating-the-direct3d9-project"></a>创建 Direct3D9 项目
 第一步是创建和配置 Direct3D9 项目。

#### <a name="to-create-the-direct3d9-project"></a>若要创建 Direct3D9 项目

1.  在名为 c + + 中创建新的 Win32 项目`D3DContent`。

     Win32 应用程序向导将打开并显示欢迎屏幕。

2.  单击 **“下一步”**。

     应用程序设置屏幕会显示。

3.  在中**应用程序类型：** 部分中，选择**DLL**选项。

4.  单击 **“完成”**。

     将生成 D3DContent 项目。

5.  在解决方案资源管理器，右键单击 D3DContent 项目并选择**属性**。

     **D3DContent 属性页**对话框随即打开。

6.  选择**C/c + +** 节点。

7.  在中**附加包含目录**字段中，指定的 DirectX 的位置包括文件夹。 此文件夹的默认位置为 %ProgramFiles%\Microsoft DirectX SDK (*版本*) \Include。

8.  双击**链接器**节点以将其展开。

9. 在中**附加库目录**字段中，指定 DirectX 库文件夹的位置。 此文件夹的默认位置为 %ProgramFiles%\Microsoft DirectX SDK (*版本*) \Lib\x86。

10. 选择**输入**节点。

11. 在中**附加依赖项**字段中，添加`d3d9.lib`和`d3dx9.lib`文件。

12. 在解决方案资源管理器，添加新模块定义文件 (.def) 名为`D3DContent.def`到项目。

## <a name="creating-the-direct3d9-content"></a>创建 Direct3D9 内容
 若要获得最佳性能，Direct3D9 内容必须使用特定的设置。 下面的代码演示如何创建具有最佳的性能特征的 Direct3D9 曲面。 有关详细信息，请参阅[Direct3D9 和 WPF 互操作性的性能注意事项](performance-considerations-for-direct3d9-and-wpf-interoperability.md)。

#### <a name="to-create-the-direct3d9-content"></a>若要创建 Direct3D9 内容

1.  使用解决方案资源管理器，将三个 c + + 类添加到名为以下的项目。

     `CRenderer` （具有虚拟析构函数）

     `CRendererManager`

     `CTriangleRenderer`

2.  在代码编辑器中打开 Renderer.h 并自动生成的代码替换为以下代码。

     [!code-cpp[System.Windows.Interop.D3DImage#RendererH](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderer.h#rendererh)]

3.  在代码编辑器中打开 Renderer.cpp 并自动生成的代码替换为以下代码。

     [!code-cpp[System.Windows.Interop.D3DImage#RendererCPP](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderer.cpp#renderercpp)]

4.  在代码编辑器中打开 RendererManager.h 并自动生成的代码替换为以下代码。

     [!code-cpp[System.Windows.Interop.D3DImage#RendererManagerH](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.h#renderermanagerh)]

5.  在代码编辑器中打开 RendererManager.cpp 并自动生成的代码替换为以下代码。

     [!code-cpp[System.Windows.Interop.D3DImage#RendererManagerCPP](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.cpp#renderermanagercpp)]

6.  在代码编辑器中打开 TriangleRenderer.h 并自动生成的代码替换为以下代码。

     [!code-cpp[System.Windows.Interop.D3DImage#TriangleRendererH](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/trianglerenderer.h#trianglerendererh)]

7.  在代码编辑器中打开 TriangleRenderer.cpp 并自动生成的代码替换为以下代码。

     [!code-cpp[System.Windows.Interop.D3DImage#TriangleRendererCPP](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/trianglerenderer.cpp#trianglerenderercpp)]

8.  在代码编辑器中打开 stdafx.h 和自动生成的代码替换为以下代码。

     [!code-cpp[System.Windows.Interop.D3DImage#StdafxH](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/stdafx.h#stdafxh)]

9. 在代码编辑器中打开 dllmain.cpp 并自动生成的代码替换为以下代码。

     [!code-cpp[System.Windows.Interop.D3DImage#DllMain](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/dllmain.cpp#dllmain)]

10. 在代码编辑器中打开 D3DContent.def。

11. 自动生成的代码替换为以下代码。

    ```
    LIBRARY "D3DContent"

    EXPORTS

    SetSize
    SetAlpha
    SetNumDesiredSamples
    SetAdapter

    GetBackBufferNoRef
    Render
    Destroy
    ```

12. 生成项目。

## <a name="next-steps"></a>后续步骤

-   承载 Direct3D9 内容在 WPF 应用程序。 有关详细信息，请参见[演练：承载 Direct3D9 内容在 WPF 中的](walkthrough-hosting-direct3d9-content-in-wpf.md)。

## <a name="see-also"></a>请参阅

- <xref:System.Windows.Interop.D3DImage>
- [Direct3D9 和 WPF 互操作性的性能注意事项](performance-considerations-for-direct3d9-and-wpf-interoperability.md)
- [演练：在 WPF 中承载 Direct3D9 内容](walkthrough-hosting-direct3d9-content-in-wpf.md)
