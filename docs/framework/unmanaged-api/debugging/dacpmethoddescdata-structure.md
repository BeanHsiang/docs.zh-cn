---
title: DacpMethodDescData 结构
ms.date: 02/01/2019
api.name:
- DacpMethodDescData Structure
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- DacpMethodDescData Structure
helpviewer.keywords:
- DacpMethodDescData Structure [.NET Framework debugging]
topic_type:
- apiref
author: hoyosjs
ms.author: juhoyosa
ms.openlocfilehash: e9037fc035693e079e2471ad37263108656b8c01
ms.sourcegitcommit: 3500c4845f96a91a438a02ef2c6b4eef45a5e2af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/07/2019
ms.locfileid: "55828582"
---
# <a name="dacpmethoddescdata-structure"></a>DacpMethodDescData 结构

定义方法的运行时信息的传输缓冲区。

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>语法

```
struct DacpMethodDescData
{
    int             bHasNativeCode;
    int             bIsDynamic;
    unsigned short  wSlotNumber;
    CLRDATA_ADDRESS NativeCodeAddr;
    CLRDATA_ADDRESS data;
    CLRDATA_ADDRESS MethodDescPtr;
    CLRDATA_ADDRESS nativeCodeInfo;
    CLRDATA_ADDRESS moduleInfo;
    mdToken         MDToken;
    CLRDATA_ADDRESS payloadGC;
    CLRDATA_ADDRESS payloadGC2;
    CLRDATA_ADDRESS managedDynamicMethodObject;
    CLRDATA_ADDRESS requestedIP;
    DacpReJitData   rejitDataCurrent;
    DacpReJitData   rejitDataRequested;
    unsigned long   cJittedRejitVersions;
};
```

## <a name="members"></a>成员

| 成员                       | 描述                                                                                     |
| ---------------------------- | ----------------------------------------------------------------------------------------------- |
| `bHasNativeCode`             | 指示运行时是否有可用于该方法的给定实例化的本机代码。 |
| `bIsDynamic`                 | 指示是否通过轻量级代码生成动态生成方法。           |
| `wSlotNumber`                | 方法的方法表中的槽数。                                                   |
| `NativeCodeAddr`             | 该方法的初始本机地址。                                                            |
| `data`                       | 指向由运行时在内部使用的缓冲区。                                             |
| `MethodDescPtr`              | 指向`MethodDesc`运行时中。                                                     |
| `nativeCodeInfo`             | 指向由运行时在内部使用，以跟踪方法的缓冲区。                            |
| `moduleInfo`                 | 模块信息由运行时在内部使用的缓冲区的指针。                      |
| `MDToken`                    | 与给定的方法相关联的标记。                                                         |
| `payloadGC`                  | 运行时在内部使用的垃圾收集缓冲区的指针。                          |
| `payloadGC2`                 | 运行时在内部使用的垃圾收集缓冲区的指针。                          |
| `managedDynamicMethodObject` | 如果该方法是动态的运行时使用此缓冲区在内部跟踪的信息。     |
| `requestedIP`                | 用于填充每个请求在给定的本机代码地址结构。                    |
| `rejitDataCurrent`           | 有关最新的检测方法版本的信息。                                   |
| `rejitDataRequested`         | Rejit 请求的本机地址信息。                                             |
| `cJittedRejitVersions`       | 该方法已通过检测 rejitted 次数。                           |


## <a name="remarks"></a>备注

此结构存在于运行时内，不通过任何标头或库文件公开。 若要使用它，如上所示定义的结构。

## <a name="requirements"></a>要求
**平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
**标头：** 无  
**库：** 无  
**.NET Framework 版本：**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>请参阅
- [调试](../../../../docs/framework/unmanaged-api/debugging/index.md)
- [调试结构](../../../../docs/framework/unmanaged-api/debugging/debugging-structures.md)
- [常见数据类型](../../../../docs/framework/unmanaged-api/common-data-types-unmanaged-api-reference.md)
