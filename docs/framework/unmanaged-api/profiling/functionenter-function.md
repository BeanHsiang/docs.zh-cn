---
title: FunctionEnter 函数
ms.date: 03/30/2017
api_name:
- FunctionEnter
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- FunctionEnter
helpviewer_keywords:
- FunctionEnter function [.NET Framework profiling]
ms.assetid: bf4ffa50-4506-4dd4-aa13-a0457b47ca74
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 886e2a81bab9fbf64668159b501a1d20180b9462
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57503094"
---
# <a name="functionenter-function"></a>FunctionEnter 函数
通知探查器控件传递给函数。  
  
> [!NOTE]
>  `FunctionEnter`函数被弃用，在.NET Framework 2.0 版中，并且它的使用将会产生对性能产生负面影响。 使用[FunctionEnter2](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md)函数。  
  
## <a name="syntax"></a>语法  
  
```  
void __stdcall FunctionEnter (  
    [in]  FunctionID funcID  
);  
```  
  
## <a name="parameters"></a>参数  
 `funcID`  
 [in]控件传递到函数的标识符。  
  
## <a name="remarks"></a>备注  
 `FunctionEnter`函数是一个回调; 必须实现它。 实现必须使用`__declspec`(`naked`) 存储类特性。  
  
 调用此函数之前，执行引擎不会保存任何寄存器。  
  
-   在进入时，必须保存使用，包括浮点单元 (FPU) 中的所有注册。  
  
-   退出时，必须通过弹出已推送到由其调用方的所有参数由还原堆栈。  
  
 实现`FunctionEnter`不应阻止，因为它会延迟垃圾回收。 实现不应尝试垃圾回收，因为堆栈可能不是在垃圾收集友好状态中。 如果尝试在垃圾回收，则运行时将阻止直到`FunctionEnter`返回。  
  
 此外，`FunctionEnter`函数不能调用到托管代码中或以任何方式导致托管的内存分配。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorProf.idl  
  
 **库：** CorGuids.lib  
  
 **.NET framework 版本：** 1.1, 1.0  
  
## <a name="see-also"></a>请参阅
- [FunctionEnter2 函数](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md)
- [FunctionLeave2 函数](../../../../docs/framework/unmanaged-api/profiling/functionleave2-function.md)
- [FunctionTailcall2 函数](../../../../docs/framework/unmanaged-api/profiling/functiontailcall2-function.md)
- [SetEnterLeaveFunctionHooks2 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-setenterleavefunctionhooks2-method.md)
- [分析全局静态函数](../../../../docs/framework/unmanaged-api/profiling/profiling-global-static-functions.md)
