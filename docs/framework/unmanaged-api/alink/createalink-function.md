---
title: CreateALink 函数
ms.date: 03/30/2017
api_name:
- CreateALink
api_location:
- alink.dll
api_type:
- DLLExport
f1_keywords:
- CreateALink
helpviewer_keywords:
- CreateALink function
- Alink API, CreateALink function
ms.assetid: fc73bcb9-6af6-44d8-bc39-2f4400325dae
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 11117db08d58684cc854400424d1836ec35b8c12
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57497999"
---
# <a name="createalink-function"></a>CreateALink 函数
创建程序集链接器的实例并设置为指定接口的指针。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT CreateALink (  
   REFIID riid,  
   IUnknown **ppInterface  
);  
```  
  
## <a name="parameters"></a>参数  
  
|参数|描述|  
|---------------|-----------------|  
|`riid`|一个程序集链接器接口的物理名称。|  
|`ppInterface`|在成功完成，包含一个指向的位置`riid`接口。|  
  
## <a name="requirements"></a>要求  
 **库**: alink.dll  
  
## <a name="see-also"></a>请参阅
- [Al.exe（程序集链接器）](../../../../docs/framework/tools/al-exe-assembly-linker.md)
