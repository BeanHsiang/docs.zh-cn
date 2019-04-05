---
title: ICorProfilerInfo3::GetRuntimeInformation 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo3.GetRuntimeInformation Method
api_location:
- Mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo3::GetRuntimeInformation
helpviewer_keywords:
- GetRuntimeInformation method [.NET Framework profiling]
- ICorProfilerInfo3::GetRuntimeInformation method [.NET Framework profiling]
ms.assetid: 4400fb8c-0407-4791-8557-f011fd2aee51
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: da116de6bde01ea7fd17f7ab27605501ae723f30
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57473002"
---
# <a name="icorprofilerinfo3getruntimeinformation-method"></a>ICorProfilerInfo3::GetRuntimeInformation 方法
提供有关所分析公共语言运行时 (CLR) 的版本信息。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT GetRuntimeInformation(  
       [out] USHORT *pClrInstanceId,  
       [out] COR_PRF_RUNTIME_TYPE *pRuntimeType,  
       [out] USHORT *pMajorVersion,  
       [out] USHORT *pMinorVersion,  
       [out] USHORT *pBuildNumber,  
       [out] USHORT *pQFEVersion,  
       [in]  ULONG  cchVersionString,  
       [out] ULONG  *pcchVersionString,  
       [out, size_is(cchVersionString), length_is(*pcchVersionString)]  
                   WCHAR  szVersionString[]);  
```  
  
## <a name="parameters"></a>参数  
 `pClrInstanceId`  
 [out]在进程中正在运行的 CLR 实例代表 ID。 这是与相同`ClrInstanceID`Windows (ETW) 启动事件的事件跟踪报告。  
  
 `pRuntimeType`  
 [out]运行时类型中。 此参数返回`COR_PRF_DESKTOP_CLR`桌面版本的 CLR，或`COR_PRF_CORE_CLR`CLR 在 Silverlight 中使用的 core 版本。  
  
 `pMajorVersion`  
 [out]CLR 主版本号。  
  
 `pMinorVersion`  
 [out]CLR 次版本号。  
  
 `pBuildVersion`  
 [out]CLR 内部版本号。  
  
 `pQFEVersion`  
 [out]与软件更新关联的 CLR 的版本号。  
  
 `cchVersionString`  
 [in]长度，以字符为单位的缓冲区的`szVersionString`指向。  
  
 `pcchVersionString`  
 [out]长度，以字符为单位的`szVersionString`。  
  
 `szVersionString`  
 [out]CLR 版本字符串。  
  
## <a name="remarks"></a>备注  
 可以传入任何参数为 null。 但是，`pcchVersionString`不能为 null 除非`szVersionString`也为 null。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorProf.idl, CorProf.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [ICorProfilerInfo3 接口](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-interface.md)
- [Profiling 接口](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [分析](../../../../docs/framework/unmanaged-api/profiling/index.md)
