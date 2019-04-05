---
title: GetALinkMessageDll 函数
ms.date: 03/30/2017
api_name:
- GetALinkMessageDll
api_location:
- alink.dll
api_type:
- DLLExport
f1_keywords:
- GetALinkMessageDll
helpviewer_keywords:
- Alink API, GetALinkMessageDll function
- GetALinkMessageDll function
ms.assetid: 67985a22-88a2-4c54-8d99-4bcde9d6213e
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 632f19e0ead57d5508265fece578bb22f18ba54a
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54722720"
---
# <a name="getalinkmessagedll-function"></a>GetALinkMessageDll 函数
查找并加载 DLL 的消息。 如果无法找到或加载 DLL 的消息，则返回 0。 消息 DLL 应在其名称是一个语言 ID、 一个子目录或当前目录中。  
  
## <a name="syntax"></a>语法  
  
```  
HINSTANCE WINAPI GetALinkMessageDll();  
```  
  
## <a name="requirements"></a>要求  
 **标头：** alink.h  
  
 **库**: alink.dll  
  
## <a name="see-also"></a>请参阅
- [Al.exe（程序集链接器）](../../../../docs/framework/tools/al-exe-assembly-linker.md)
