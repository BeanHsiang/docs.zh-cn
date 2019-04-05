---
title: 优化性能：利用硬件
ms.date: 03/30/2017
helpviewer_keywords:
- graphics [WPF], performance
- hardware rendering pipeline [WPF]
- rendering tiers [WPF]
- graphics rendering tiers [WPF]
- graphics [WPF], rendering tiers
- software rendering pipeline [WPF]
ms.assetid: bfb89bae-7aab-4cac-a26c-a956eda8fce2
ms.openlocfilehash: 1e0050dbf6ec5ade22e3f09ceee66f69826e56df
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57374253"
---
# <a name="optimizing-performance-taking-advantage-of-hardware"></a>优化性能：利用硬件
内部体系结构[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]具有两个呈现管道、 硬件和软件。 本主题提供有关这些呈现管道，以帮助你做出有关您的应用程序的性能优化的信息。  
  
## <a name="hardware-rendering-pipeline"></a>硬件呈现管道  
 在确定的最重要因素之一[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]性能是它是呈现绑定 — 必须要呈现，成本更高性能的像素越多。 但是，呈现的详细信息可以卸载到[!INCLUDE[TLA#tla_gpu](../../../../includes/tlasharptla-gpu-md.md)]，可以获得更多的性能优势。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]应用程序的硬件呈现管道采用充分利用[!INCLUDE[TLA#tla_dx](../../../../includes/tlasharptla-dx-md.md)]功能支持的最少的硬件上[!INCLUDE[TLA#tla_dx](../../../../includes/tlasharptla-dx-md.md)]版本 7.0。 支持的硬件可以获得更多优化[!INCLUDE[TLA#tla_dx](../../../../includes/tlasharptla-dx-md.md)]版本 7.0 和 PixelShader 2.0 + 功能。  
  
## <a name="software-rendering-pipeline"></a>软件呈现管道  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]软件呈现管道是完全受 CPU 限制。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 充分利用 SSE 和 SSE2 指令的设置在 CPU 中来实现优化、 功能完备的软件光栅器。 回退到软件是无缝应用程序功能不能使用硬件呈现管道呈现任何时间。  
  
 您会遇到的最大的性能问题时在软件模式下呈现相关填充率，定义为呈现的像素数。 如果担心软件呈现模式中的性能，尝试尽量减少重新绘制像素的次数。 例如，如果您的应用程序包含一个蓝色背景，然后通过它呈现略有透明图像，您将呈现所有两次，应用程序中的像素。 因此，它将需要两次长呈现具有比有仅蓝色背景图像的应用程序。  
  
### <a name="graphics-rendering-tiers"></a>图形呈现层  
 它可能很难预测你的应用程序将在运行的硬件配置。 但是，你可能想要考虑使用允许无缝切换功能在不同的硬件上运行时，以便它可以充分利用每个不同的硬件配置的应用程序的设计。  
  
 若要实现此目的，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]提供功能，以确定在运行时中的系统的图形功能。 分类为一个三个呈现功能层的视频卡取决于图形功能。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 公开[!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)]允许应用程序在查询的呈现功能层。 然后，你的应用程序可以在运行的时间，具体取决于硬件支持的呈现层采用不同的代码路径。  
  
 对呈现层级别影响最大的图形硬件功能包括：  
  
-   **视频 RAM** - 图形硬件中的视频内存量决定了可用于合成图形的缓冲区大小和数量。  
  
-   **像素着色器** - 像素着色器是基于像素计算效果的图形处理功能。 每个显示帧可能有数百万像素需要处理，具体取决于显示图形的分辨率。  
  
-   **顶点着色器** - 顶点着色器是对对象的顶点数据执行数学运算的图形处理功能。  
  
-   **多纹理支持** - 多纹理支持是指对 3D 图形对象执行混合操作期间应用两个或更多个不同纹理的功能。 多纹理支持的程度取决于图形硬件中的多纹理单元数。  
  
 像素着色器、 顶点着色器和多纹理功能用于定义特定[!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)]版本级别，这反过来，用于定义中的不同的呈现层[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]。  
  
 图形硬件的功能决定了 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序的呈现功能。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 系统定义了 3 个呈现层：  
  
-   **呈现层 0** - 无图形硬件加速。 [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)]版本级别低于 7.0 版。  
  
-   **呈现层 1**部分的图形硬件加速。 [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)]版本级别为大于或等于版本 7.0，并**较小**比 9.0 版。  
  
-   **呈现层 2** - 大多数图形功能都使用图形硬件加速。 [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)] 版本级别高于或等于 9.0。  
  
 有关详细信息[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]呈现层，请参阅[图形呈现层](graphics-rendering-tiers.md)。  
  
## <a name="see-also"></a>请参阅
- [优化 WPF 应用程序性能](optimizing-wpf-application-performance.md)
- [规划应用程序性能](planning-for-application-performance.md)
- [布局和示例](optimizing-performance-layout-and-design.md)
- [2D 图形和图像处理](optimizing-performance-2d-graphics-and-imaging.md)
- [对象行为](optimizing-performance-object-behavior.md)
- [应用程序资源](optimizing-performance-application-resources.md)
- [文本](optimizing-performance-text.md)
- [数据绑定](optimizing-performance-data-binding.md)
- [其他性能建议](optimizing-performance-other-recommendations.md)
