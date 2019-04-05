---
title: ICorProfilerCallback8::DynamicMethodJITCompilationStarted 方法
ms.date: 04/10/2018
api_name:
- ICorProfilerCallback8.DynamicMethodJITCompilationStarted
api_location:
- mscorwks.dll
- corprof.idl
api_type:
- COM
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 170d0b20069724a4e1845be0250b2897daa10dee
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57501235"
---
# <a name="icorprofilercallback8dynamicmethodjitcompilationstarted-method"></a>ICorProfilerCallback8::DynamicMethodJITCompilationStarted 方法
[.NET Framework 4.7 和更高版本中受支持]  
  
通知探查器时的动态方法的 JIT 编译已启动。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT DynamicMethodJITCompilationStarted(  
     [in]  FunctionID  functionId,   
     [in]  BOOL        fIsSafeToBlock,   
     [in]  LPCBYTE     pILHeader,   
     [in]  LONG        cbILHeader   
);  
```  
  
## <a name="parameters"></a>参数  
[in] `functionId`  
内存中函数的 JIT 编译开始的标识符。   

[in] `fIsSafeToBlock`   
`true` 若要指示，阻止可能会导致运行时等待调用的线程返回从此回调;`false`以指示，阻止不会影响运行时的操作。  

[in] `pILHeader`    
指向方法的 IL 标头的第一个字节的指针。   

[in] `cbILHeader`    
IL 标头中的字节数。 

## <a name="remarks"></a>备注  

JIT 编译动态方法时，将触发此回调。 这包括各种 IL 存根 （stub） 和 LCG 方法。 其目标是向探查器编写器提供足够的信息来标识用户的已编译的方法。

> [!NOTE]
> `functionId` 值不能用来解析为其元数据标记，因为动态方法不具有任何元数据。

`pILHeader`指针回调期间才有效。

## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorProf.idl, CorProf.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  
  
## <a name="see-also"></a>请参阅
- [DynamicMethodJITCompilationFinished 方法](icorprofilercallback8-dynamicmethodjitcompilationfinished-method.md)
- [ICorProfilerCallback8 接口](icorprofilercallback8-interface.md)
