---
title: pInvokeStackImbalance MDA
ms.date: 03/30/2017
helpviewer_keywords:
- signatures, platform invoke
- stack depth
- platform invoke stack imbalance
- MDAs (managed debugging assistants), platform invoke
- platform invoke, run-time errors
- PInvokeStackImbalance MDA
- managed debugging assistants (MDAs), platform invoke
ms.assetid: 34ddc6bd-1675-4f35-86aa-de1645d5c631
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 9ecdfd708217f260b0c02383159fab88948029c6
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54512311"
---
# <a name="pinvokestackimbalance-mda"></a>PInvokeStackImbalance MDA

`PInvokeStackImbalance`托管调试助手 (MDA) 当 CLR 检测到平台 invoke 调用之后的堆栈深度与预期的堆栈深度，给定中指定的调用约定不匹配时激活<xref:System.Runtime.InteropServices.DllImportAttribute>属性和托管签名中的参数声明。

仅为 32 位 x86 平台实现 `PInvokeStackImbalance` MDA。

> [!NOTE]
> `PInvokeStackImbalance`默认情况下禁用 MDA。 在 Visual Studio 2017 中， `PInvokeStackImbalance` MDA 将出现在**托管调试助手**列表中**异常设置**对话框中 (其中显示当你选择**调试** >  **Windows** > **异常设置**)。 但是，选中或清除**中断时引发**复选框不会启用或禁用 MDA; 它仅控制在 MDA 处于激活状态时，Visual Studio 是否引发异常。

## <a name="symptoms"></a>症状

进行平台 invoke 调用时或之后，应用程序会遭遇访问冲突或内存损坏。

## <a name="cause"></a>原因

平台 invoke 调用的托管签名可能不匹配正在被调用的方法的非托管签名。  这种不匹配可能是由于没有声明参数的正确数量或没有指定参数的适当大小的托管签名所导致的。  MDA 也可因调用约定（可能由 <xref:System.Runtime.InteropServices.DllImportAttribute> 属性指定）不匹配非托管调用约定而激活。

## <a name="resolution"></a>解决方法

检查托管平台调用签名和调用约定，以确认它与本机目标的签名和调用约定匹配。  请尝试在托管端和非托管端上显式指定调用约定。 非托管函数也可能（尽管可能性不太大）出于某种原因（例如非托管编译器中的 bug）使堆栈不平衡。

## <a name="effect-on-the-runtime"></a>对运行时的影响

强制所有平台 invoke 调用都采用 CLR 中的非优化路径。

## <a name="output"></a>输出

MDA 消息会提供正导致堆栈不平衡的平台 invoke 方法调用的名称。 方法 `SampleMethod` 上的平台 invoke 调用的示例消息为：

**PInvoke 函数 SampleMethod 的调用具有使堆栈不平衡。这可能是因为托管的 PInvoke 签名与非托管的目标签名不匹配。检查的调用约定和 PInvoke 签名的参数匹配的目标的非托管的签名。**

## <a name="configuration"></a>配置

```xml
<mdaConfig>
  <assistants>
    <pInvokeStackImbalance />
  </assistants>
</mdaConfig>
```

## <a name="see-also"></a>请参阅

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [使用托管调试助手诊断错误](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)
- [互操作封送处理](../../../docs/framework/interop/interop-marshaling.md)
