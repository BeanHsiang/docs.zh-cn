---
title: ICorProfilerCallback::Shutdown 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.Shutdown
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::Shutdown
helpviewer_keywords:
- ICorProfilerCallback::Shutdown method [.NET Framework profiling]
- Shutdown method [.NET Framework profiling]
ms.assetid: 1ea194f0-a331-4855-a2ce-37393b8e5f84
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: bb2bfe927eddaf6812b0185a586135e76f649c1b
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54728117"
---
# <a name="icorprofilercallbackshutdown-method"></a>ICorProfilerCallback::Shutdown 方法
通知探查器正在关闭应用程序。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT Shutdown();  
```  
  
## <a name="remarks"></a>备注  
 探查器代码不能安全地调用的方法[ICorProfilerInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)接口后`Shutdown`调用方法。 对任何调用`ICorProfilerInfo`方法会导致未定义的行为后`Shutdown`方法返回。 某些不可变事件可能仍会发生后关闭;请注意探查器应发生这种情况时立即返回。  
  
 `Shutdown`作为托管代码所分析的托管应用程序启动时，才会调用方法 （即，托管进程堆栈上的初始帧）。 如果应用程序作为非托管代码启动，但稍后又跳转到托管代码，从而创建公共语言运行时 (CLR) 的实例则`Shutdown`将不会调用。 对于这些情况下，探查器应包含在其库中`DllMain`例程使用 DLL_PROCESS_DETACH 值以释放任何资源并执行清理处理数据，例如刷新跟踪磁盘，等等。  
  
 一般情况下，探查器必须处理意外关闭。 例如，进程可能会暂停通过 Win32 的`TerminateProcess`方法 （在 Winbase.h 中声明）。 在其他情况下，CLR 将暂停特定托管的线程 （后台线程），而无需为其提供有序销毁消息。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorProf.idl, CorProf.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [ICorProfilerCallback 接口](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
- [Initialize 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-initialize-method.md)
