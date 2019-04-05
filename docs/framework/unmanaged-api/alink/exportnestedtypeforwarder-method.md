---
title: ExportNestedTypeForwarder 方法
ms.date: 03/30/2017
api_name:
- IALink.ExportNestedTypeForwarder
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- ExportNestedTypeForwarder
helpviewer_keywords:
- ExportNestedTypeForwarder method
ms.assetid: 886ea6c5-6b26-4b88-8bf6-448d6d191950
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: ed615ea641293f8ea3fdf962e3f84d602934df60
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57494683"
---
# <a name="exportnestedtypeforwarder-method"></a>ExportNestedTypeForwarder 方法
将嵌套类型的类型转发器添加到给定的程序集的 type 表。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT ExportNestedTypeForwarder(  
    mdAssembly      AssemblyID,  
    mdToken         FileToken,  
    mdTypeDef       TypeToken,  
    mdExportedType  ParentType,  
    LPCWSTR         pszTypename,  
    DWORD           dwFlags,  
    mdExportedType* pType  
) PURE;  
```  
  
## <a name="parameters"></a>参数  
 `AssemblyID`  
 要从导出的程序集的 ID。  
  
 `FileToken`  
 标记或程序集的文件 ID 定义的类型的文件。  
  
 `TypeToken`  
 类型的标记。  
  
 `ParentType`  
 父类型的令牌。  
  
 `pszTypename`  
 若要导出的完全限定的类型名称。  
  
 `dwFlags`  
 `ComType` 标志，如`tdPublic`或`tdNested`。  
  
 `pType`  
 收到的导出类型的令牌。 这是只需将发出嵌套的类型。  
  
## <a name="return-value"></a>返回值  
 如果该方法成功，返回，则为 S_OK。  
  
## <a name="requirements"></a>要求  
 需要 alink.h  
  
## <a name="see-also"></a>请参阅
- [IALink 接口](../../../../docs/framework/unmanaged-api/alink/ialink-interface.md)
- [IALink2 接口](../../../../docs/framework/unmanaged-api/alink/ialink2-interface.md)
- [ALink API](../../../../docs/framework/unmanaged-api/alink/index.md)
