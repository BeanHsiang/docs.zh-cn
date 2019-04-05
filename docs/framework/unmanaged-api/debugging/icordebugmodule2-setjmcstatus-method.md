---
title: ICorDebugModule2::SetJMCStatus 方法
ms.date: 03/30/2017
api_name:
- ICorDebugModule2.SetJMCStatus
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule2::SetJMCStatus
helpviewer_keywords:
- SetJMCStatus method, ICorDebugModule2 interface [.NET Framework debugging]
- ICorDebugModule2::SetJMCStatus method [.NET Framework debugging]
ms.assetid: 8c6d2089-4dbb-4715-b9e9-2a4491c8c9ce
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d20c640d6a6a43b7bde4c7d46df470c7bc8c5aa2
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57499519"
---
# <a name="icordebugmodule2setjmcstatus-method"></a>ICorDebugModule2::SetJMCStatus 方法
所有类的所有方法只是我的代码 (JMC) 状态设置为指定的值，除中此 ICorDebugModule2 中`pTokens`数组，它将设置为相反值。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT SetJMCStatus (  
    [in] BOOL                        bIsJustMyCode,  
    [in] ULONG32                     cTokens,  
    [in, size_is(cTokens)] mdToken   pTokens[]  
);  
```  
  
## <a name="parameters"></a>参数  
 `bIsJustMycode`  
 [in]设置为`true`的代码是调试; 否则为如果设置为`false`。  
  
 `cTokens`  
 [in] `pTokens` 数组的大小。  
  
 `pTokens`  
 [in]一个数组`mdToken`值，其中每个引用的方法，将具有其 JMC 状态设置为 ！`bIsJustMycode`。  
  
## <a name="remarks"></a>备注  
 中指定每个方法的 JMC 状态`pTokens`数组设置为相反`bIsJustMycode`值。 在此模块中的所有其他方法的状态设置为`bIsJustMycode`值。  
  
 `SetJMCStatus`方法会清除所有以前的 JMC 设置在此模块中。  
  
 `SetJMCStatus`方法返回 S_OK HRESULT，如果已成功设置的所有函数。 它将返回标记一些函数，如果将 CORDBG_E_FUNCTION_NOT_DEBUGGABLE HRESULT`true`不是可调试。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
