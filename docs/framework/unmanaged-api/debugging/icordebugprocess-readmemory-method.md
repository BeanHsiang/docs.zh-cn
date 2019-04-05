---
title: ICorDebugProcess::ReadMemory 方法
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.ReadMemory
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::ReadMemory
helpviewer_keywords:
- ReadMemory method [.NET Framework debugging]
- ICorDebugProcess::ReadMemory method [.NET Framework debugging]
ms.assetid: 28e4b2f6-9589-445c-be24-24a3306795e7
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 218279684304b766a9bf009f5891ac4910254a3c
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57492161"
---
# <a name="icordebugprocessreadmemory-method"></a>ICorDebugProcess::ReadMemory 方法
读取此进程的内存的指定的区域。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT ReadMemory(  
    [in]  CORDB_ADDRESS address,   
    [in]  DWORD size,  
    [out, size_is(size), length_is(size)] BYTE buffer[],  
    [out] SIZE_T *read);  
```  
  
## <a name="parameters"></a>参数  
 `address`  
 [in]一个`CORDB_ADDRESS`值，该值指定要读取的内存的基址。  
  
 `size`  
 [in]要从内存读取的字节数。  
  
 `buffer`  
 [out]该缓冲区用于接收内存的内容。  
  
 `read`  
 [out]到指定的缓冲区传输到的字节数的指针。  
  
## <a name="remarks"></a>备注  
 `ReadMemory`方法主要用于通过互操作调试用于检查正在使用的调试对象的非托管部分的内存区域。 此方法还可以用于读取 Microsoft 中间语言 (MSIL) 代码和 JIT 编译的本机代码。  
  
 将从中返回的数据中删除任何托管的断点`buffer`参数。 为本机断点集将进行任何调整[ICorDebugProcess2::SetUnmanagedBreakpoint](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess2-setunmanagedbreakpoint-method.md)。  
  
 执行进程内存没有缓存。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
