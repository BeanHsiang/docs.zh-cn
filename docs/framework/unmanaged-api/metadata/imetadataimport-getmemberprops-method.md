---
title: IMetaDataImport::GetMemberProps 方法
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetMemberProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetMemberProps
helpviewer_keywords:
- IMetaDataImport::GetMemberProps method [.NET Framework metadata]
- GetMemberProps method [.NET Framework metadata]
ms.assetid: 42790918-4142-4938-b8f4-a56979a55846
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: fa1fa59bf3bb33e115989eae9095752eea00a041
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57487637"
---
# <a name="imetadataimportgetmemberprops-method"></a>IMetaDataImport::GetMemberProps 方法
获取有关指定的成员定义，包括名称、 二进制签名和相对虚拟地址的元数据中存储的信息<xref:System.Type>指定的元数据标记所引用的成员。 这是一个简单的帮助程序方法： 如果*mb*然后是 MethodDef **GetMethodProps**调用; 如果*mb*然后是 FieldDef **GetFieldProps**调用。 查看这些详细信息的其他方法。 
  
## <a name="syntax"></a>语法  
  
```  
HRESULT GetMemberProps (  
   [in]  mdToken           mb,   
   [out] mdTypeDef         *pClass,  
   [out] LPWSTR            szMember,   
   [in]  ULONG             cchMember,   
   [out] ULONG             *pchMember,   
   [out] DWORD             *pdwAttr,  
   [out] PCCOR_SIGNATURE   *ppvSigBlob,   
   [out] ULONG             *pcbSigBlob,   
   [out] ULONG             *pulCodeRVA,   
   [out] DWORD             *pdwImplFlags,   
   [out] DWORD             *pdwCPlusTypeFlag,   
   [out] UVCP_CONSTANT     *ppValue,  
   [out] ULONG             *pcchValue  
);  
```  
  
## <a name="parameters"></a>参数  
 `mb`  
 [in]引用的成员，若要获取有关关联的元数据标记。  
  
 `pClass`  
 [out]指向表示类的成员的元数据标记的指针。  
  
 `szMember`  
 [out]成员的名称。  
  
 `cchMember`  
 [in]在宽字符为单位的大小`szMember`缓冲区。  
  
 `pchMember`  
 [out]在宽字符返回的名称的大小。  
  
 `pdwAttr`  
 [out]任何标志应用于的成员的值。  
  
 `ppvSigBlob`  
 [out]指向成员的二进制元数据签名的指针。  
  
 `pcbSigBlob`  
 [out]以字节为单位的大小`ppvSigBlob`。  
  
 `pulCodeRVA`  
 [out]指向成员的相对虚拟地址的指针。  
  
 `pdwImplFlags`  
 [out]与成员关联的任何方法实现标志。  
  
 `pdwCPlusTypeFlag`  
 [out]一个标志，用于将标记<xref:System.ValueType>。 它是之一`ELEMENT_TYPE_*`值。
  
 `ppValue`  
 [out]返回此成员的常量字符串值。  
  
 `pcchValue`  
 [out]以字符为单位的大小`ppValue`，或为零`ppValue`不保存字符串。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Cor.h  
  
 **库：** 包含为 MsCorEE.dll 中的资源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [IMetaDataImport 接口](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2 接口](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
