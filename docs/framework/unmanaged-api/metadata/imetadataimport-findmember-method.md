---
title: IMetaDataImport::FindMember 方法
ms.date: 03/30/2017
api_name:
- IMetaDataImport.FindMember
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::FindMember
helpviewer_keywords:
- IMetaDataImport::FindMember method [.NET Framework metadata]
- FindMember method [.NET Framework metadata]
ms.assetid: ad32fb84-c2b6-41cd-888d-787ff3a90449
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 777d7bf51db3e6984f30e31c46ac115301d13faf
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57478968"
---
# <a name="imetadataimportfindmember-method"></a>IMetaDataImport::FindMember 方法
获取一个指针 MemberDef 标记的字段或方法都包含由指定<xref:System.Type>并具有指定的名称和元数据签名。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT FindMember (  
   [in]  mdTypeDef         td,  
   [in]  LPCWSTR           szName,   
   [in]  PCCOR_SIGNATURE   pvSigBlob,   
   [in]  ULONG             cbSigBlob,   
   [out] mdToken           *pmb  
);  
```  
  
## <a name="parameters"></a>参数  
 `td`  
 [in]对类或包含要搜索的成员的接口的 TypeDef 标记。 如果此值为`mdTokenNil`，全局变量或全局函数执行查找。  
  
 `szName`  
 [in]要搜索的成员的名称。  
  
 `pvSigBlob`  
 [in]指向成员的二进制元数据签名的指针。  
  
 `cbSigBlob`  
 [in]以字节为单位的大小`pvSigBlob`。  
  
 `pmb`  
 [out]指向匹配的 MemberDef 标记的指针。  
  
## <a name="remarks"></a>备注  
 指定使用封闭类或接口的成员 (`td`)，其名称 (`szName`)，并根据需要它的签名 (`pvSigBlob`)。 可能有多个具有相同名称的类或接口中的成员。 在这种情况下，将传递到唯一的匹配项的成员的签名。  
  
 签名传递给`FindMember`必须已生成在当前范围内，因为这些签名将绑定到特定的作用域。 签名可以嵌入令牌，用于标识封闭类或值类型。 令牌的本地 TypeDef 表中的索引。 不能生成上下文的当前作用域外部的运行时签名并使用该签名一样的输入`FindMember`。  
  
 `FindMember` 查找直接在类或接口; 中定义的成员找不到继承的成员。  
  
> [!NOTE]
>  `FindMember` 是一个帮助器方法。 它将调用[imetadataimport:: Findmethod](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-findmethod-method.md); 如果该调用未找到匹配项，`FindMember`然后调用[imetadataimport:: Findfield](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-findfield-method.md)。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Cor.h  
  
 **库：** 包含为 MsCorEE.dll 中的资源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [IMetaDataImport 接口](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2 接口](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
