---
title: 规划应用程序性能
ms.date: 03/30/2017
helpviewer_keywords:
- applications [WPF], optimizing
- WPF application [WPF], optimizing
ms.assetid: c91bd0c5-a193-46ff-9da1-eb7a3a76a3b3
ms.openlocfilehash: fda5330ff75c1744f3ed9d4394e51b5efb737071
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57374422"
---
# <a name="planning-for-application-performance"></a>规划应用程序性能
实现性能目标的成功取决于如何开发您性能的策略。 规划是在开发的任何产品的第一个阶段。 本主题介绍一些非常简单规则可用于开发良好的性能策略。  
  
## <a name="think-in-terms-of-scenarios"></a>方案会想到  
 方案可帮助你专注于你的应用程序的关键组件。 方案通常派生自你的客户，以及竞争对手的产品。 始终研究你的客户，并找出真正让他们高兴您的产品和竞争对手的产品。 客户的反馈可以帮助您确定应用程序的主要方案。 例如，如果您要设计一个组件，将使用在启动时，很可能，在应用程序启动时只有一次调用该组件。 启动时间将成为你的密钥方案。 关键方案的其他示例可能是所需的帧速率对于动画序列，或最大工作集允许的应用程序。  
  
## <a name="define-goals"></a>定义目标  
 目标可帮助您确定应用程序的性能加快或减慢。 应为每个方案定义目标。 您定义的所有性能目标应都基于客户的预期。 它可能很难制定性能在早期目标应用程序开发周期，仍有很多未解决的问题。 但是，最好设置一个初始目标和更高版本而不是将一个目标根本修改。  
  
## <a name="understand-your-platform"></a>了解你的平台  
 始终保持度量、 调查、 在应用程序开发周期中简化/更正的周期。 从开始到开发周期结束时，需要可靠、 稳定的环境中的应用程序的性能进行测量。 应避免通过外部因素造成的变化。 例如，测试性能时，应禁用防病毒软件或任何自动更新功能 （如 SMS)，顺序不会对性能造成影响的测试结果。 你已经度量出应用程序的性能，需要标识将导致最大的改进的更改。 一次修改了你的应用程序，再次启动该周期。  
  
## <a name="make-performance-tuning-an-iterative-process"></a>进行性能优化一个迭代过程  
 您应该知道将使用每个功能的相对成本。 例如，Microsoft.NET Framework 中对反射的使用通常是占用大量的计算资源，因此要明智地使用它。 这并不意味着若要避免使用反射，仅，你应该注意平衡应用程序的性能要求，你使用的功能的性能要求。  
  
## <a name="build-towards-graphical-richness"></a>生成大量图形的内容  
 创建对实现可缩放方法的一项关键技术[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]应用程序的性能是构建出图形的丰富性和复杂性。 始终使用最少的性能密集型资源来实现您的方案的目标开始。 后实现这些目标，请使用更多性能密集型功能，始终记住你方案的目标构建出图形丰富功能。 请记住，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]是一个非常丰富的平台，提供了非常丰富的图形功能。 使用无需多想性能密集型功能可以对应用程序总体性能产生负面影响。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件是本质上是可扩展的从而对广泛自定义其外观，而不修改其控件行为。 通过利用样式、 数据模板和控件模板，可以创建并以增量方式发展可自定义[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]的适应你的性能要求。  
  
## <a name="see-also"></a>请参阅
- [优化 WPF 应用程序性能](optimizing-wpf-application-performance.md)
- [利用硬件](optimizing-performance-taking-advantage-of-hardware.md)
- [布局和示例](optimizing-performance-layout-and-design.md)
- [2D 图形和图像处理](optimizing-performance-2d-graphics-and-imaging.md)
- [对象行为](optimizing-performance-object-behavior.md)
- [应用程序资源](optimizing-performance-application-resources.md)
- [文本](optimizing-performance-text.md)
- [数据绑定](optimizing-performance-data-binding.md)
- [其他性能建议](optimizing-performance-other-recommendations.md)
