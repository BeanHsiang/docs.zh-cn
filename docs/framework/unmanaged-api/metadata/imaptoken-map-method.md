---
title: IMapToken::Map 方法
ms.date: 03/30/2017
api_name:
- IMapToken.Map
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMapToken::Map
helpviewer_keywords:
- IMapToken::Map method [.NET Framework metadata]
- Map method [.NET Framework metadata]
ms.assetid: b9b4bf2f-1098-43d6-9619-a99b4bda1940
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: ece12247e48a0a005fd542bf76a32a1c6eeaa7cb
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57478397"
---
# <a name="imaptokenmap-method"></a>IMapToken::Map 方法
映射使用元数据签名的程序集之间的关系。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT Map (  
    [in]  mdToken tkImp,   
    [in]  mdToken tkEmit  
);  
```  
  
## <a name="parameters"></a>参数  
 `tkImp`  
 [in]表示导入的代码对象的元数据标记。  
  
 `tkEmit`  
 [in]表示发出的代码对象的元数据标记。  
  
## <a name="remarks"></a>备注  
 标记重新映射发生在合并期间时, 原始令牌的作用域导入 （源） 元数据范围内，新的令牌的范围限定在发出 （目标） 的元数据范围内。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Cor.h  
  
 **库：** 用作 MsCorEE.dll 中的资源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [IMapToken 接口](../../../../docs/framework/unmanaged-api/metadata/imaptoken-interface.md)
