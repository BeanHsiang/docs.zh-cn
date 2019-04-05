---
title: StackSnapshotCallback 函数
ms.date: 03/30/2017
api_name:
- StackSnapshotCallback
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- StackSnapshotCallback
helpviewer_keywords:
- StackSnapshotCallback function [.NET Framework profiling]
ms.assetid: d0f235b2-91fe-4f82-b7d5-e5c64186eea8
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 43e71696282a3c9e6d25793b583ee19f306e167b
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57486233"
---
# <a name="stacksnapshotcallback-function"></a>StackSnapshotCallback 函数
提供有关每个托管的帧和非托管帧的每次运行在堆栈上的堆栈遍历，启动的过程信息，以及探查器[ICorProfilerInfo2::DoStackSnapshot](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md)方法。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT __stdcall StackSnapshotCallback (  
    [in] FunctionID funcId,  
    [in] UINT_PTR ip,  
    [in] COR_PRF_FRAME_INFO frameInfo,  
    [in] ULONG32 contextSize,  
    [in] BYTE context[],  
    [in] void *clientData  
);  
```  
  
## <a name="parameters"></a>参数  
 `funcId`  
 [in]如果此值为零，此回叫是运行非托管帧;否则为它是托管函数的标识符，并且此回叫是个托管帧。  
  
 `ip`  
 [in]在框架中的本机代码指令指针的值。  
  
 `frameInfo`  
 [in]一个`COR_PRF_FRAME_INFO`引用有关堆栈帧的信息的值。 仅在此回调期间，此值是有效使用。  
  
 `contextSize`  
 [in]大小`CONTEXT`结构，它引用的`context`参数。  
  
 `context`  
 [in]一个指向 Win32`CONTEXT`结构，它表示此帧的 CPU 的状态。  
  
 `context`参数才有效，仅当传入的 COR_PRF_SNAPSHOT_CONTEXT 标志`ICorProfilerInfo2::DoStackSnapshot`。  
  
 `clientData`  
 [in]指向客户端数据，直接通过传递从`ICorProfilerInfo2::DoStackSnapshot`。  
  
## <a name="remarks"></a>备注  
 `StackSnapshotCallback`由探查器编写器实现函数。 您必须限制中完成工作的复杂性`StackSnapshotCallback`。 例如，在使用`ICorProfilerInfo2::DoStackSnapshot`以异步方式，，目标线程可能会持有锁。 如果中的代码`StackSnapshotCallback`需要同一个锁死锁可能会随之发生。  
  
 `ICorProfilerInfo2::DoStackSnapshot`方法调用`StackSnapshotCallback`函数一次每个托管帧或一次每次运行的非托管帧。 如果`StackSnapshotCallback`称为非托管帧的运行，探查器可能使用寄存器上下文 (所引用的`context`参数) 来执行其自己的非托管的堆栈遍历。 在此情况下，Win32`CONTEXT`结构表示非托管帧的运行中最近推送的帧的 CPU 的状态。 尽管 Win32`CONTEXT`结构包括所有寄存器的值，但您应依赖于的堆栈指针寄存器、 帧指针寄存器、 指令指针寄存器和非易失性 （即保留） 的值仅整数寄存器。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorProf.idl  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [DoStackSnapshot 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md)
- [分析全局静态函数](../../../../docs/framework/unmanaged-api/profiling/profiling-global-static-functions.md)
