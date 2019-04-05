---
title: Windows 窗体控件中的多线程处理
ms.date: 03/30/2017
helpviewer_keywords:
- BackgroundWorker component
- threading [Windows Forms], controls
ms.assetid: c311d652-0f26-45fa-bdcc-b1615d73ce4e
ms.openlocfilehash: cc7f358a62c8057abb77e1f5a28544bb6c858d98
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57703317"
---
# <a name="multithreading-in-windows-forms-controls"></a>Windows 窗体控件中的多线程处理
在许多应用程序，您可以进行用户界面 (UI) 响应速度更快执行耗时的操作，另一个线程上。 有多种工具都是可用于多线程 Windows 窗体控件，包括<xref:System.Threading>命名空间，<xref:System.Windows.Forms.Control.BeginInvoke%2A?displayProperty=nameWithType>方法，和`BackgroundWorker`组件。  
  
> [!NOTE]
>  `BackgroundWorker`组件替换，并添加了功能<xref:System.Threading>命名空间和<xref:System.Windows.Forms.Control.BeginInvoke%2A?displayProperty=nameWithType>方法; 但是，这些将保留向后兼容性和将来使用，如果您选择。 有关详细信息，请参阅[BackgroundWorker 组件概述](backgroundworker-component-overview.md)。  
  
## <a name="in-this-section"></a>本节内容  
 [如何：对 Windows 窗体控件进行线程安全调用](how-to-make-thread-safe-calls-to-windows-forms-controls.md)  
 演示如何对 Windows 窗体控件进行线程安全调用。  
  
 [如何：使用后台线程搜索文件](how-to-use-a-background-thread-to-search-for-files.md)  
 演示如何使用<xref:System.Threading>命名空间和<xref:System.Windows.Forms.Control.BeginInvoke%2A>方法以异步方式搜索文件。  
  
## <a name="reference"></a>参考  
 <xref:System.ComponentModel.BackgroundWorker>  
 文档组件，用于封装工作线程进行异步操作。  
  
 <xref:System.Media.SoundPlayer.LoadAsync%2A>  
 介绍如何以异步方式加载声音。  
  
 <xref:System.Windows.Forms.PictureBox.LoadAsync%2A>  
 介绍如何以异步方式加载图像。  
  
## <a name="related-sections"></a>相关章节  
 [如何：在后台运行操作](how-to-run-an-operation-in-the-background.md)  
 演示如何执行耗时的操作与<xref:System.ComponentModel.BackgroundWorker>组件。  
  
 [BackgroundWorker 组件概述](backgroundworker-component-overview.md)  
 提供一些主题，介绍如何使用<xref:System.ComponentModel.BackgroundWorker>组件进行异步操作。
