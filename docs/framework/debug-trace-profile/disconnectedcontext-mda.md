---
title: disconnectedContext MDA
ms.date: 03/30/2017
helpviewer_keywords:
- DisconnectedContext MDA
- MDAs (managed debugging assistants), disconnected context
- dead context
- transitioning disconnected apartment or context
- context disconnections
- managed debugging assistants (MDAs), disconnected context
ms.assetid: 1887d31d-7006-4491-93b3-68fd5b05f71d
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 8f125d322a5a3e2841d6b1ba1f2f8d5fe9745870
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54569698"
---
# <a name="disconnectedcontext-mda"></a>disconnectedContext MDA
如果 CLR 在处理关于 COM 对象的请求时尝试转换到断开连接的单元或上下文，将激活 `disconnectedContext` 托管调试助手 (MDA)。  
  
## <a name="symptoms"></a>症状  
 将对[运行时可调通包装器](../../../docs/framework/interop/runtime-callable-wrapper.md) (RCW) 的调用发送到当前单元或上下文中的基础 COM 组件，而不是发送到调用所在的 COM 组件。 如果该 COM 组件不是多线程的（例如，在单线程单元 (STA) 组件的情况中），则将导致损坏或数据丢失。 或者，如果 RCW 本身是一个代理，则该调用可能会引发 HRESULT 为 RPC_E_WRONG_THREAD 的 <xref:System.Runtime.InteropServices.COMException>。  
  
## <a name="cause"></a>原因  
 当 CLR 尝试转换为 OLE 单元或上下文时，OLE 单元或上下文已关闭。 最常见的原因是：在 STA 单元拥有的所有 COM 组件完全释放之前，STA 单元已经关闭。在用户代码对 RCW 进行显式调用时或在 CLR 自行操作 COM 组件时（例如，在对关联的 RCW 进行了垃圾回收后，CLR 释放 COM 组件），可能会发生这种情况。  
  
## <a name="resolution"></a>解决方法  
 若要避免发生此问题，请确保在应用程序处理完单元中存在的所有对象之前，拥有 STA 的线程不会终止。 这也同样适用于上下文；请确保在应用程序处理完上下文中存在的所有 COM 组件之前，上下文不会关闭。  
  
## <a name="effect-on-the-runtime"></a>对运行时的影响  
 此 MDA 对 CLR 无任何影响。 它只报告有关断开连接的上下文的数据。  
  
## <a name="output"></a>输出  
 报告断开连接的单元或上下文的上下文 Cookie。  
  
## <a name="configuration"></a>配置  
  
```xml  
<mdaConfig>  
  <assistants>  
    <disconnectedContext />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>请参阅
- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [使用托管调试助手诊断错误](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)
- [互操作封送处理](../../../docs/framework/interop/interop-marshaling.md)
