---
title: ICorProfilerInfo::SetILInstrumentedCodeMap 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.SetILInstrumentedCodeMap
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::SetILInstrumentedCodeMap
helpviewer_keywords:
- ICorProfilerInfo::SetILInstrumentedCodeMap method [.NET Framework profiling]
- SetILInstrumentedCodeMap method [.NET Framework profiling]
ms.assetid: bce1dcf8-b4ec-4e73-a917-f2df1ad49c8a
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: bc13dc1348a6d397c86b03976c86c3595f749cf6
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57480060"
---
# <a name="icorprofilerinfosetilinstrumentedcodemap-method"></a>ICorProfilerInfo::SetILInstrumentedCodeMap 方法
设置指定的函数使用指定的 Microsoft 中间语言 (MSIL) 的映射条目的代码图。  
  
> [!NOTE]
>  在.NET Framework 2.0 版中，调用`SetILInstrumentedCodeMap`上`FunctionID`表示泛型函数在特定应用程序域中，将会影响应用程序域中该函数的所有实例。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT SetILInstrumentedCodeMap(  
    [in]  FunctionID functionId,  
    [in]  BOOL       fStartJit,  
    [in]  ULONG      cILMapEntries,  
    [in, size_is(cILMapEntries)] COR_IL_MAP rgILMapEntries[]);  
```  
  
## <a name="parameters"></a>参数  
 `functionId`  
 [in]若要设置代码映射的函数的 ID。  
  
 `fStartJit`  
 [in]一个布尔值，该值指示是否在调用`SetILInstrumentedCodeMap`方法是为特定的第一个`FunctionID`。 设置`fStartJit`到`true`在首次调用`SetILInstrumentedCodeMap`为给定`FunctionID`，并对其`false`之后。  
  
 `cILMapEntries`  
 [in]中的元素数`cILMapEntries`数组。  
  
 `rgILMapEntries`  
 [in]COR_IL_MAP 结构数组，其中每个指定的 MSIL 偏移量。  
  
## <a name="remarks"></a>备注  
 探查器通常插入语句的源代码中的一种方法，以实现该方法 （例如，若要在达到给定的源行时通知）。 `SetILInstrumentedCodeMap` 允许探查器将原始的 MSIL 指令映射到其新位置。 可以使用探查器[icorprofilerinfo:: Getiltonativemapping](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getiltonativemapping-method.md)方法以获取原始的 MSIL 偏移量为给定的本机偏移量。  
  
 调试器将假定每个旧的偏移量指 MSIL 偏移的原始未修改 MSIL 代码中，并且，每个新的偏移量是指在新的、 已检测代码的 MSIL 偏移量。 映射应按升序排序。 单步执行才能正常工作，请遵循以下准则：  
  
-   不对重新排序已检测的 MSIL 代码。  
  
-   不要删除原始的 MSIL 代码。  
  
-   在映射中包括的程序数据库 (PDB) 文件中的所有序列点的条目。 映射不会插入缺失的条目。 因此，如果给定以下映射：  
  
     (0，0 个新)  
  
     (5，10 个新)  
  
     (9 旧，20 个新)  
  
    -   旧的偏移量为 0、 1、 2、 3 或 4 将映射到新偏移量为 0。  
  
    -   旧的偏移量为 5、 6、 7 或 8 将映射到新偏移量为 10。  
  
    -   旧的偏移量为 9 或更高版本将映射到新偏移量为 20。  
  
    -   新的偏移量为 0、 1、 2、 3、 4、 5、 6、 7、 8 或 9 将映射到旧偏移量为 0。  
  
    -   新的偏移 10、 11、 12、 13、 14、 15、 16、 17、 18 或 19 的将映射到旧偏移量为 5。  
  
    -   为 20 或更高版本的新偏移量将映射到旧偏移量为 9。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorProf.idl, CorProf.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v11plus](../../../../includes/net-current-v11plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [ICorProfilerInfo 接口](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
