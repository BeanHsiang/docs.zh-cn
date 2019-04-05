---
title: IMetaDataImport::GetEventProps 方法
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetEventProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetEventProps
helpviewer_keywords:
- IMetaDataImport::GetEventProps method [.NET Framework metadata]
- GetEventProps method [.NET Framework metadata]
ms.assetid: 5eaf3b4a-92b7-4d5b-97e0-1e83721e0052
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6f2eec9fce1909f6a83190f5ba3e99162461bbc4
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57492148"
---
# <a name="imetadataimportgeteventprops-method"></a>IMetaDataImport::GetEventProps 方法
获取由指定的事件标记，包括声明类型、 添加和删除方法的委托，任何标志及其他关联的数据所表示的事件的元数据信息。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT GetEventProps (  
   [in]  mdEvent       ev,  
   [out] mdTypeDef     *pClass,   
   [out] LPCWSTR       szEvent,   
   [in]  ULONG         cchEvent,   
   [out] ULONG         *pchEvent,   
   [out] DWORD         *pdwEventFlags,  
   [out] mdToken       *ptkEventType,  
   [out] mdMethodDef   *pmdAddOn,   
   [out] mdMethodDef   *pmdRemoveOn,   
   [out] mdMethodDef   *pmdFire,   
   [out] mdMethodDef   rmdOtherMethod[],   
   [in]  ULONG         cMax,  
   [out] ULONG         *pcOtherMethod  
);  
```  
  
## <a name="parameters"></a>参数  
 `ev`  
 [in]表示要获取的元数据的事件的事件元数据标记。  
  
 `pClass`  
 [out]指向表示声明事件的类的 TypeDef 标记的指针。  
  
 `szEvent`  
 [out]引用的事件名称`ev`。  
  
 `pchEvent`  
 [in]请求的长度以宽字符为单位`szEvent`。  
  
 `pdwEventFlags`  
 [out]中的宽字符返回的长度`szEvent`。  
  
 `ptkEventType`  
 [out]一个指向 TypeRef 或 TypeDef 元数据令牌表示<xref:System.Delegate>事件的类型。  
  
 `pmdAddOn`  
 [out]指向表示为事件添加处理程序的方法的元数据标记的指针。  
  
 `pmdRemoveOn`  
 [out]指向表示移除事件处理程序的方法的元数据标记的指针。  
  
 `pmdFire`  
 [out]指向表示引发事件的方法的元数据标记的指针。  
  
 `rmdOtherMethod`  
 [out]与其他方法与事件关联的令牌指针的数组。  
  
 `cMax`  
 [in] `rmdOtherMethod` 数组的最大大小。  
  
 `pcOtherMethod`  
 [out]在返回的标记数`rmdOtherMethod`。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Cor.h  
  
 **库：** 包含为 MsCorEE.dll 中的资源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [IMetaDataImport 接口](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2 接口](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
