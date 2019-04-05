---
title: ICorDebugProcess::WriteMemory 方法
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.WriteMemory
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::WriteMemory
helpviewer_keywords:
- ICorDebugProcess::WriteMemory method [.NET Framework debugging]
- WriteMemory method [.NET Framework debugging]
ms.assetid: d5c07d86-045d-4391-893b-0bcd2959f90e
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2e9d640fb1c9dae5bb195baa504e560ba8e45821
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57497088"
---
# <a name="icordebugprocesswritememory-method"></a>ICorDebugProcess::WriteMemory 方法
将数据写入到的此过程中的内存区域。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT WriteMemory(  
    [in]  CORDB_ADDRESS address,  
    [in]  DWORD size,  
    [in, size_is(size)] BYTE buffer[],  
    [out] SIZE_T *written);  
```  
  
## <a name="parameters"></a>参数  
 `address`  
 [in]一个`CORDB_ADDRESS`写入数据的内存区域的基址的值。 在传输数据之前，系统将验证开始的位置的基址的指定大小的内存区域可以进行写入访问。 如果不能访问，该方法将失败。  
  
 `size`  
 [in]要写入到的内存区域的字节数。  
  
 `buffer`  
 [in]包含要写入的数据的缓冲区。  
  
 `written`  
 [out]指向一个变量来接收此过程中的内存区域写入的字节数的指针。 如果`written`为 NULL，则忽略此参数。  
  
## <a name="remarks"></a>备注  
 任何断点后自动写入数据。 在.NET Framework 2.0 版中，本机调试器应使用此方法用于将断点注入到指令流。 使用[ICorDebugProcess2::SetUnmanagedBreakpoint](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess2-setunmanagedbreakpoint-method.md)相反。  
  
 `WriteMemory`应仅之外托管代码使用方法。 如果使用不当，则此方法会损坏运行时。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
