---
title: IMetaDataImport::FindField 方法
ms.date: 03/30/2017
api_name:
- IMetaDataImport.FindField
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::FindField
helpviewer_keywords:
- IMetaDataImport::FindField method [.NET Framework metadata]
- FindField method [.NET Framework metadata]
ms.assetid: 38cd4e16-fbb2-471c-aa73-ac51a1931ad2
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 4a6f2e428366d2fe96313879ef1256d7b86ddd29
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57490406"
---
# <a name="imetadataimportfindfield-method"></a>IMetaDataImport::FindField 方法
获取指向 FieldDef 标记字段包含由指定<xref:System.Type>并具有指定的名称和元数据签名。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT FindField (  
   [in]  mdTypeDef         td,  
   [in]  LPCWSTR           szName,  
   [in]  PCCOR_SIGNATURE   pvSigBlob,  
   [in]  ULONG             cbSigBlob,  
   [out] mdFieldDef        *pmb  
);  
```  
  
## <a name="parameters"></a>参数  
 `td`  
 [in]对类或接口，包含要搜索的字段的 TypeDef 标记。 如果此值为`mdTokenNil`，在执行查找的全局变量。  
  
 `szName`  
 [in]要搜索的字段的名称。  
  
 `pvSigBlob`  
 [in]一个指向该字段的二进制元数据签名。  
  
 `cbSigBlob`  
 [in]以字节为单位的大小`pvSigBlob`。  
  
 `pmb`  
 [out]指向匹配的 FieldDef 标记的指针。  
  
## <a name="remarks"></a>备注  
 指定使用封闭类或接口的字段 (`td`)，其名称 (`szName`)，并根据需要它的签名 (`pvSigBlob`)。  
  
 签名传递给`FindField`必须已生成在当前范围内，因为这些签名将绑定到特定的作用域。 签名可以嵌入令牌，用于标识封闭类或值类型。 （该标记是本地的 TypeDef 表中的索引）。 无法生成上下文的当前作用域外部的运行时签名并使用该签名作为输入`FindField`。  
  
 `FindField` 查找直接在类或接口; 中定义的字段找不到继承的字段。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Cor.h  
  
 **库：** 包含为 MsCorEE.dll 中的资源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [IMetaDataImport 接口](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2 接口](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
