---
title: GetTypeLibInfo 函数
ms.date: 03/30/2017
api_name:
- GetTypeLibInfo
api_location:
- TlbRef.dll
api_type:
- DLLExport
f1_keywords:
- GetTypeLibInfo
helpviewer_keywords:
- GetTypeLibInfo function [.NET Framework]
ms.assetid: a1c4d165-9bdc-4ca8-940e-292d4ffcc338
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 88516a5ab7fa6ce3cd27422b32cb467a94f50f92
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57492772"
---
# <a name="gettypelibinfo-function"></a>GetTypeLibInfo 函数
返回有关指定的类型库的信息通过检查其[TLIBATTR](https://docs.microsoft.com/previous-versions/windows/desktop/api/oaidl/ns-oaidl-tagtlibattr)结构。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT GetTypeLibInfo(  
    [in]   LPWSTR     szFile,  
    [out]  GUID      *pTypeLibID,  
    [out]  LCID      *pTypeLibLCID,  
    [out]  SYSKIND   *pTypeLibPlatform,  
    [out]  USHORT    *pTypeLibMajorVer,  
    [out]  USHORT    *pTypeLibMinorVer  
);  
```  
  
## <a name="parameters"></a>参数  
 `szFile`  
 [in]类型库文件名称。  
  
 `pTypeLibID`  
 [out]类型库的 GUID。  
  
 `pTypeLibLCID`  
 [out]类型库的本地化 ID。  
  
 `pTypeLibPlatform`  
 [out]一个[SYSKIND](https://docs.microsoft.com/previous-versions/windows/desktop/api/oaidl/ne-oaidl-tagsyskind)标识目标操作系统的类型库的标志。 常见的值为 SYS_WIN32 和 SYS_WIN64。  
  
 `pTypeLibMajorVer`  
 [out]类型库的主版本号。 例如，对于版本*x.y*，主版本号是*x*。  
  
 `pTypeLibMinorVer`  
 [out]类型库的次版本号。 例如，对于版本*x.y*的次版本号是*y*。  
  
## <a name="remarks"></a>备注  
 `GetTypeLibInfo`调用函数[Tlbexp.exe （类型库导出程序）](../../../../docs/framework/tools/tlbexp-exe-type-library-exporter.md)。 此工具生成类型库描述公共语言运行时 (CLR) 程序集中的类型。  
  
 如果任何参数为 null，该函数返回`HRESULT`的`E_POINTER`。 否则，它将返回 `S_OK`。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** TlbRef.h  
  
 **库：** TlbRef.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [Tlbexp Helper 函数](../../../../docs/framework/unmanaged-api/tlbexp/index.md)
- [LoadTypeLibEx 函数](https://docs.microsoft.com/previous-versions/windows/desktop/api/oleauto/nf-oleauto-loadtypelibex)
