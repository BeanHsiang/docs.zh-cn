---
title: IEnumRAWINPUTDEVICE
ms.date: 03/30/2017
helpviewer_keywords:
- IEnumRAWINPUTDEVICE interface [WPF]
ms.assetid: 88c8b389-a48b-46b9-b895-8ed7b1e26fea
ms.openlocfilehash: e7bc6f2c96413f3898a17b541733eeecd6a260f7
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57375059"
---
# <a name="ienumrawinputdevice"></a>IEnumRAWINPUTDEVICE
此接口枚举原始输入设备，并仅供 PresentationHost.exe 使用。  
  
> [!NOTE]
>  此 API 预期仅支持在本地客户端计算机上使用  
  
## <a name="members"></a>成员  
  
|成员|描述|  
|------------|-----------------|  
|[IEnumRAWINPUTDEVIC:Next](ienumrawinputdevic-next.md)|在枚举器列表中枚举下一个 `celt` 元素（即 RAWINPUTDEVICE 结构），将它们和 `rgelt` 中枚举元素的实际数量返回至 `pceltFetched`。|  
|[IEnumRAWINPUTDEVIC:Skip](ienumrawinputdevic-skip.md)|指示枚举器跳过下一步`celt`枚举中的元素，以便下次调用[IEnumRAWINPUTDEVIC:Next](ienumrawinputdevic-next.md)不会返回这些元素。|  
|[IEnumRAWINPUTDEVIC:Reset](ienumrawinputdevic-reset.md)|将枚举序列重置到开头。|  
|[IEnumRAWINPUTDEVIC:Clone](ienumrawinputdevic-clone.md)|创建一个与当权枚举器相同状态的原始输入设备枚举器，以循环访问相同的列表。|  
  
## <a name="see-also"></a>请参阅
- [关于原始输入](/windows/desktop/inputdev/about-raw-input)
