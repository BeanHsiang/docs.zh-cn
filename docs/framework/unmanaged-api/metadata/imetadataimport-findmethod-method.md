---
title: IMetaDataImport::FindMethod 方法
ms.date: 03/30/2017
api_name:
- IMetaDataImport.FindMethod
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::FindMethod
helpviewer_keywords:
- FindMethod method [.NET Framework metadata]
- IMetaDataImport::FindMethod method [.NET Framework metadata]
ms.assetid: 0f9bde1d-e306-438d-941b-d0925b322304
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 857ea06ad8aba2a6de87bdf670ad0462a2f7dde1
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57487275"
---
# <a name="imetadataimportfindmethod-method"></a>IMetaDataImport::FindMethod 方法
获取指向 MethodDef 标记所用的方法由指定<xref:System.Type>并具有指定的名称和元数据签名。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT FindMethod (  
   [in]  mdTypeDef          td,  
   [in]  LPCWSTR            szName,   
   [in]  PCCOR_SIGNATURE    pvSigBlob,   
   [in]  ULONG              cbSigBlob,   
   [out] mdMethodDef        *pmb  
);  
```  
  
## <a name="parameters"></a>参数  
 `td`  
 [in]`mdTypeDef`标记，表示包含要搜索的成员的类型 （类或接口）。 如果此值为`mdTokenNil`，则会对全局函数执行查找。  
  
 `szName`  
 [in]要搜索的方法的名称。  
  
 `pvSigBlob`  
 [in]指向方法的二进制元数据签名的指针。  
  
 `cbSigBlob`  
 [in]以字节为单位的大小`pvSigBlob`。  
  
 `pmb`  
 [out]指向匹配的 MethodDef 标记的指针。  
  
## <a name="remarks"></a>备注  
 指定使用封闭类或接口的方法 (`td`)，其名称 (`szName`)，并根据需要它的签名 (`pvSigBlob`)。 可能有多个具有相同名称的类或接口中的方法。 在这种情况下，传递方法的签名，以查找唯一匹配项。  
  
 签名传递给`FindMethod`必须已生成在当前范围内，因为这些签名将绑定到特定的作用域。 签名可以嵌入令牌，用于标识封闭类或值类型。 令牌的本地 TypeDef 表中的索引。 不能生成上下文的当前作用域外部的运行时签名并使用该签名一样的输入`FindMethod`。  
  
 `FindMethod` 查找直接在类或接口; 中定义的方法找不到继承的方法。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Cor.h  
  
 **库：** 包含为 MsCorEE.dll 中的资源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Reflection.MethodInfo>
- [IMetaDataImport 接口](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2 接口](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
