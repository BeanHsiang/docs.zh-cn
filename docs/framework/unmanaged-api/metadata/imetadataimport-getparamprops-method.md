---
title: IMetaDataImport::GetParamProps 方法
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetParamProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetParamProps
helpviewer_keywords:
- IMetaDataImport::GetParamProps method [.NET Framework metadata]
- GetParamProps method [.NET Framework metadata]
ms.assetid: 4d5e5f00-bcab-4f41-b191-176511a186a7
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: ed9bae4fde96f0878e40ed73b81cc8776571ada5
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57468053"
---
# <a name="imetadataimportgetparamprops-method"></a>IMetaDataImport::GetParamProps 方法
获取指定的 ParamDef 标记所引用的参数的元数据值。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT GetParamProps (  
   [in]  mdParamDef      tk,  
   [out] mdMethodDef     *pmd,  
   [out] ULONG           *pulSequence,  
   [out] LPWSTR          szName,  
   [in]  ULONG           cchName,  
   [out] ULONG           *pchName,  
   [out] DWORD           *pdwAttr,  
   [out] DWORD           *pdwCPlusTypeFlag,  
   [out] UVCP_CONSTANT   *ppValue,  
   [out] ULONG           *pcchValue  
);  
```  
  
## <a name="parameters"></a>参数  
 `tk`  
 [in]表示要返回的元数据的参数的 ParamDef 标记。  
  
 `pmd`  
 [out]指向表示采用参数的方法的 MethodDef 标记的指针。  
  
 `pulSequence`  
 [out]参数的方法参数列表中的序号位置。  
  
 `szName`  
 [out]用于保存参数的名称的缓冲区。  
  
 `cchName`  
 [in]请求的大小以宽字符为单位`szName`。  
  
 `pchName`  
 [out]在宽字符为单位返回的大小`szName`。  
  
 `pdwAttr`  
 [out]一个指向任何与参数关联的特性标志。 这是一个位掩码的`CorParamAttr`值。  
  
 `pdwCPlusTypeFlag`  
 [out]该参数是指向一个标志，用于指定的指针<xref:System.ValueType>。  
  
 `ppValue`  
 [out]指向常量字符串的参数返回的指针。  
  
 `pcchValue`  
 [out]大小`ppValue`宽字符，或者，如果零`ppValue`不保存字符串。  
  
## <a name="remarks"></a>备注

中的顺序值`pulSequence`参数 1 开头。 返回值具有的序列号为 0。

## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Cor.h  
  
 **库：** 包含为 MsCorEE.dll 中的资源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [IMetaDataImport 接口](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2 接口](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
