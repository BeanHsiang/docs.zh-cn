---
title: COR_GC_STATS 结构
ms.date: 03/30/2017
api_name:
- COR_GC_STATS
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- COR_GC_STATS
helpviewer_keywords:
- COR_GC_STATS structure [.NET Framework hosting]
ms.assetid: 8d4ff73e-739b-40f6-9349-359fbc99c2f9
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3fc212321b28545f62f0a1c2965281d02ac73e40
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54638101"
---
# <a name="corgcstats-structure"></a>COR_GC_STATS 结构
提供有关垃圾回收机制的公共语言运行时 (CLR) 的统计信息。  
  
## <a name="syntax"></a>语法  
  
```  
typedef struct _COR_GC_STATS {  
    ULONG   Flags;   
    SIZE_T  ExplicitGCCount;  
    SIZE_T  GenCollectionsTaken[3];  
    SIZE_T  CommittedKBytes;   
    SIZE_T  ReservedKBytes;  
    SIZE_T  Gen0HeapSizeKBytes;  
    SIZE_T  Gen1HeapSizeKBytes;  
    SIZE_T  Gen2HeapSizeKBytes;  
    SIZE_T  LargeObjectHeapSizeKBytes;  
    SIZE_T  KBytesPromotedFromGen0;  
    SIZE_T  KBytesPromotedFromGen1;  
} COR_GC_STATS;  
```  
  
## <a name="members"></a>成员  
  
|成员|描述|  
|------------|-----------------|  
|`Flags`|指示应计算的字段值，并将其返回。|  
|`ExplicitGCCount`|指示由外部请求已强制垃圾回收的数目。|  
|`GenCollectionsTaken`|指示为每个代所执行的垃圾回收次数。|  
|`CommittedKBytes`|提交所有堆中的千字节为单位的总数。|  
|`ReservedKBytes`|保留所有堆中的千字节为单位的总数。|  
|`Gen0HeapSizeKBytes`|以千字节单位零代堆大小。|  
|`Gen1HeapSizeKBytes`|以千字节，第一代堆的大小。|  
|`Gen2HeapSizeKBytes`|以千字节，第 2 代堆的大小。|  
|`LargeObjectHeapSizeKBytes`|以千字节，大型对象堆的大小。|  
|`KBytesPromotedFromGen0`|大小，以千字节为单位，从第 0 代提升到第一代的对象。|  
|`KBytesPromotedFromGen1`|大小，以千字节为单位，从第一代提升到第 2 代的对象。|  
  
## <a name="remarks"></a>备注  
 [Iclrgcmanager:: Getstats](../../../../docs/framework/unmanaged-api/hosting/iclrgcmanager-getstats-method.md)方法需要`Flags`字段`COR_GC_STATS`设置为一个或多个值的结构[COR_GC_STAT_TYPES](../../../../docs/framework/unmanaged-api/hosting/cor-gc-stat-types-enumeration.md)枚举来指定该统计信息是设置。  
  
 下表将映射到两个此结构提供的统计信息[COR_GC_STAT_TYPES](../../../../docs/framework/unmanaged-api/hosting/cor-gc-stat-types-enumeration.md)枚举值`COR_GC_COUNTS`和`COR_GC_MEMORYUSAGE`。  
  
|指定的 COR_GC_COUNTS|指定的 COR_GC_MEMORYUSAGE|  
|----------------------------------|---------------------------------------|  
|`ExplicitGCCount`<br /><br /> `GenCollectionsTaken`|`CommittedKBytes`<br /><br /> `ReservedKBytes`<br /><br /> `Gen0HeapSizeKBytes`<br /><br /> `Gen1HeapSizeKBytes`<br /><br /> `Gen2HeapSizeKBytes`<br /><br /> `LargeObjectHeapSizeKBytes`<br /><br /> `KBytesPromotedFromGen0`<br /><br /> `KBytesPromotedFromGen1`|  
  
 该用法的示例如下所示：  
  
```  
COR_GC_STATS GCStats;  
GCStats.Flags = COR_GC_COUNTS | COR_GC_MEMORYUSAGE;  
pCLRGCManager->GetStats(&GCStats);  
```  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** GCHost.idl  
  
 **库：** 包含为 MSCorEE.dll 中的资源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [承载结构](../../../../docs/framework/unmanaged-api/hosting/hosting-structures.md)
- [自动内存管理](../../../../docs/standard/automatic-memory-management.md)
- [垃圾回收](../../../../docs/standard/garbage-collection/index.md)
