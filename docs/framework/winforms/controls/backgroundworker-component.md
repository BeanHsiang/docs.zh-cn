---
title: BackgroundWorker 组件
ms.date: 03/30/2017
helpviewer_keywords:
- BackgroundWorker component
- background tasks
- Asynchronous Pattern
- forms [Windows Forms], multithreading
- components [Windows Forms], asynchronous
- forms [Windows Forms], background operations
- threading [Windows Forms], background operations
- background operations
ms.assetid: bef7b0ab-ce57-475a-a2d6-fb8a702a9417
ms.openlocfilehash: 0baf54d27cf33eef7e4df7019ee98b42eba40205
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57710662"
---
# <a name="backgroundworker-component"></a>BackgroundWorker 组件
`BackgroundWorker`组件使您的窗体或控件以异步方式运行操作。  
  
## <a name="in-this-section"></a>本节内容  
 [BackgroundWorker 组件概述](backgroundworker-component-overview.md)  
 介绍`BackgroundWorker`组件，使您能够执行耗时的操作以异步方式 （"在后台"），在不同于应用程序的主 UI 线程的线程。  
  
 [演练：在后台运行操作](walkthrough-running-an-operation-in-the-background.md)  
 演示如何使用`BackgroundWorker`组件在设计器中运行单独的线程上一个耗时的操作。  
  
 [如何：在后台运行操作](how-to-run-an-operation-in-the-background.md)  
 演示如何使用`BackgroundWorker`组件来运行单独的线程上一个耗时的操作。  
  
 [演练：实现使用后台操作的窗体](walkthrough-implementing-a-form-that-uses-a-background-operation.md)  
 创建使用异步执行数学运算的设计器的应用程序。  
  
 [如何：实现使用后台操作的窗体](how-to-implement-a-form-that-uses-a-background-operation.md)  
 创建以异步方式执行数学计算的应用程序。  
  
 [如何：下载在后台中的文件](how-to-download-a-file-in-the-background.md)  
 演示如何使用`BackgroundWorker`组件下载单独的线程上的文件。  
  
## <a name="reference"></a>参考  
 <xref:System.ComponentModel.BackgroundWorker>  
 对此类进行描述，并提供指向其所有成员的链接。  
  
 <xref:System.ComponentModel.RunWorkerCompletedEventArgs>  
 介绍了保存的数据的类型<xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted>事件。  
  
 <xref:System.ComponentModel.ProgressChangedEventArgs>  
 介绍了保存的数据的类型<xref:System.ComponentModel.BackgroundWorker.ProgressChanged>事件。  
  
## <a name="related-sections"></a>相关章节  
 [基于事件的异步模式概述](../../../standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)  
 介绍如何异步模式提供多线程应用程序的优点而隐藏的许多复杂多线程设计中固有的问题。
