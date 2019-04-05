---
title: ICorDebugFunction2::GetVersionNumber 方法
ms.date: 03/30/2017
api_name:
- ICorDebugFunction2.GetVersionNumber
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFunction2::GetVersionNumber
helpviewer_keywords:
- ICorDebugFunction2::GetVersionNumber method [.NET Framework debugging]
- GetVersionNumber method, ICorDebugFunction2 interface [.NET Framework debugging]
ms.assetid: e3a1ce48-9bb9-4ed6-a5fe-5e1819a6333f
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6cc9c2af62184c83857b82445941f6087a05c2c3
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57497166"
---
# <a name="icordebugfunction2getversionnumber-method"></a>ICorDebugFunction2::GetVersionNumber 方法
获取此函数的编辑并继续版本。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT GetVersionNumber (  
    [out] ULONG32   *pnVersion  
);  
```  
  
## <a name="parameters"></a>参数  
 `pnVersion`  
 [out]指向一个整数，表示由此 ICorDebugFunction2 对象的函数的版本号的指针。  
  
## <a name="remarks"></a>备注  
 跟踪在调试会话期间为每个模块所进行的编辑次数的运行时。 一个函数的版本编号是一个超过数目的引入了函数的编辑。 函数的原始版本是版本 1。 该数字递增模块每次都[ICorDebugModule2::ApplyChanges](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule2-applychanges-method.md)调用该模块。 因此，如果函数的主体已对的第一个和第三个调用中替换`ICorDebugModule2::ApplyChanges`，`GetVersionNumber`可能会返回版本 1、 2 或 4 表示该函数，但没有版本 3。 （该函数会有任何版本 3。）  
  
 对于每个模块中分别跟踪的版本号。 因此，如果你在第 1 单元，并对模块 2 未执行四个编辑，第 1 单元在下一次编辑将到第 1 单元中的所有已编辑函数分配版本号为 6。 如果编辑收尾工作了模块 2 相同，第 2 单元中的函数将获得 2 的版本号。  
  
 通过获取版本号`GetVersionNumber`方法可能会低于通过获取[icordebugfunction:: Getcurrentversionnumber](../../../../docs/framework/unmanaged-api/debugging/icordebugfunction-getcurrentversionnumber-method.md)。  
  
 [Icordebugcode:: Getversionnumber](../../../../docs/framework/unmanaged-api/debugging/icordebugcode-getversionnumber-method.md)方法执行相同的操作`ICorDebugFunction2::GetVersionNumber`。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
