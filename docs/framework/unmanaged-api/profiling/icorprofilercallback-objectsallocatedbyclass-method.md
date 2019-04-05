---
title: ICorProfilerCallback::ObjectsAllocatedByClass 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ObjectsAllocatedByClass
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ObjectsAllocatedByClass
helpviewer_keywords:
- ObjectsAllocatedByClass method [.NET Framework profiling]
- ICorProfilerCallback::ObjectsAllocatedByClass method [.NET Framework profiling]
ms.assetid: 91d688f3-a80e-419d-9755-ff94bc04188a
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: e26e7ac9b89e005d9520ad860cf3acee7d3cc6cc
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57479748"
---
# <a name="icorprofilercallbackobjectsallocatedbyclass-method"></a>ICorProfilerCallback::ObjectsAllocatedByClass 方法
通知探查器有关的最新的垃圾回收以来已创建的每个指定的类的实例数。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT ObjectsAllocatedByClass(  
    [in] ULONG   cClassCount,  
    [in, size_is(cClassCount)] ClassID classIds[] ,  
    [in, size_is(cClassCount)] ULONG   cObjects[] );  
```  
  
## <a name="parameters"></a>参数  
 `cClassCount`  
 [in]大小`classIds`和`cObjects`数组。  
  
 `classIds`  
 [in]类 Id，其中每个 ID 指定的类具有一个或多个实例的数组。  
  
 `cObjects`  
 [in]一个整数，其中每个整数指定中的相应类的实例数数组`classIds`数组。  
  
## <a name="remarks"></a>备注  
 `classIds`和`cObjects`数组是并行数组。 例如，`classIds[i]`和`cObjects[i]`引用同一个类。 如果自上次垃圾回收以来创建的类没有实例，则省略类。 `ObjectsAllocatedByClass`回调不会报告大型对象堆中分配的对象。  
  
 通过报告的数字`ObjectsAllocatedByClass`只是估计。 对于精确计数，请使用[icorprofilercallback:: Objectallocated](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-objectallocated-method.md)。  
  
 `classIds`数组可能包含一个或多个 null 项，如果相应`cObjects`数组具有正在卸载的类型。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorProf.idl, CorProf.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [ICorProfilerCallback 接口](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
