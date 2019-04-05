---
title: ICorDebugModule2::ApplyChanges 方法
ms.date: 03/30/2017
api_name:
- ICorDebugModule2.ApplyChanges
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule2::ApplyChanges
helpviewer_keywords:
- ApplyChanges method [.NET Framework debugging]
- ICorDebugModule2::ApplyChanges method [.NET Framework debugging]
ms.assetid: 96fa3406-6a6f-41a1-88c6-d9bc5d1a16d1
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ab0e28bd21b66f370a1a1e82359fe474574fd7bb
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57481569"
---
# <a name="icordebugmodule2applychanges-method"></a>ICorDebugModule2::ApplyChanges 方法
适用于正在运行的进程中元数据的更改和 Microsoft 中间语言 (MSIL) 代码中的更改。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT ApplyChanges (  
    [in] ULONG                       cbMetadata,  
    [in, size_is(cbMetadata)] BYTE   pbMetadata[],  
    [in] ULONG                       cbIL,  
    [in, size_is(cbIL)] BYTE         pbIL[]  
);  
```  
  
## <a name="parameters"></a>参数  
 `cbMetadata`  
 [in]以字节为单位的增量元数据的大小。  
  
 `pbMetadata`  
 [in]包含增量元数据的缓冲区。 从返回的缓冲区的地址[IMetaDataEmit2::SaveDeltaToMemory](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-savedeltatomemory-method.md)方法。  
  
 元数据中的相对虚拟地址 (Rva) 应是 MSIL 代码开头的相对路径。  
  
 `cbIL`  
 [in]大小，以字节为单位的增量 MSIL 代码。  
  
 `pbIL`  
 [in]包含更新的 MSIL 代码的缓冲区。  
  
## <a name="remarks"></a>备注  
 `pbMetadata`参数是特殊的增量元数据格式 (通过为输出[IMetaDataEmit2::SaveDeltaToMemory](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-savedeltatomemory-method.md))。 `pbMetadata` 采用作为基的上一个元数据，描述要应用于此基本的单个更改。  
  
 与此相反， `pbIL[`] 参数包含的更新的方法的新 MSIL，并且应彻底替换该方法的上一个 MSIL  
  
 调试程序时在调试器的内存中已创建增量 MSIL 和元数据，调用`ApplyChanges`发送到公共语言运行时 (CLR) 的更改。 运行时更新其元数据的表、 将新的 MSIL 放入进程，并设置新的 MSIL 中实时 (JIT) 编译。 应用所做的更改后，应调用调试器[IMetaDataEmit2::ResetENCLog](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-resetenclog-method.md)准备的下一个编辑会话。 然后，调试器可能会继续执行过程。  
  
 每当调试器调用`ApplyChanges`对具有增量元数据的模块，它还应调用[imetadataemit:: Applyeditandcontinue](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-applyeditandcontinue-method.md)与在该模块的元数据除外复制其副本的所有相同的增量元数据用于发出所做的更改。 如果元数据的副本以某种方式将成为同步扩展使用的实际元数据，调试器可以始终丢弃该副本并获取新副本。  
  
 如果`ApplyChanges`方法失败，则调试会话处于无效状态，且必须重新启动。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
