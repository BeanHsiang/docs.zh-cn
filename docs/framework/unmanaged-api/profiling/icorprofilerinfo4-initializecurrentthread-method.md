---
title: ICorProfilerInfo4::InitializeCurrentThread 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo4::InitializeCurrentThread
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo4::InitializeCurrentThread
helpviewer_keywords:
- ICorProfilerInfo4::InitializeCurrentThread method [.NET Framework profiling]
- InitializeCurrentThread method, ICorProfilerInfo4 interface [.NET Framework profiling]
ms.assetid: 18a3335c-8c75-476c-b6de-72c0bfedae5d
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 990ae316a780af9be96f6b91900f33cbb2db4f36
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54727971"
---
# <a name="icorprofilerinfo4initializecurrentthread-method"></a>ICorProfilerInfo4::InitializeCurrentThread 方法
初始化当前线程提前后续探查器在同一线程调用的 API，因此可以避免该死锁。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT InitializeCurrentThread ();  
```  
  
## <a name="remarks"></a>备注  
 我们建议您调用`InitializeCurrentThread`API 存在时将调用探查器的任何线程上挂起线程。 此方法通常由采样探查器可创建自己的线程调用[ICorProfilerInfo2::DoStackSnapshot](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md)方法来执行堆栈遍历目标线程被挂起时。 通过调用`InitializeCurrentThread`探查器后当探查器首先创建采样线程，可以确保每个线程迟缓初始化 CLR 将执行在第一次调用期间`DoStackSnapshot`现在可以发生的安全时没有其他线程是挂起。  
  
> [!NOTE]
>  `InitializeCurrentThread` 执行初始化提前以完成任务采用锁，并可能发生死锁。 调用`InitializeCurrentThread`仅当没有任何挂起的线程时。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorProf.idl, CorProf.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [ICorProfilerInfo4 接口](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-interface.md)
- [Profiling 接口](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [分析](../../../../docs/framework/unmanaged-api/profiling/index.md)
