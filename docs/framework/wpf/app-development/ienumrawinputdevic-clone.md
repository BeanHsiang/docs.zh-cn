---
title: IEnumRAWINPUTDEVIC:Clone
ms.date: 03/30/2017
helpviewer_keywords:
- Clone method [WPF]
ms.assetid: 2a6a1900-aa55-45fa-9382-241d569a2dc4
ms.openlocfilehash: abc8a6e4780c8fe50afcf1b04f7e14aeb6452704
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57485403"
---
# <a name="ienumrawinputdevicclone"></a>IEnumRAWINPUTDEVIC:Clone
创建一个与当权枚举器相同状态的原始输入设备枚举器，以循环访问相同的列表。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT Clone( [out] IEnumRAWINPUTDEVICE **ppenum);  
```  
  
## <a name="parameters"></a>参数  
 `ppenum`  
  
 [out]接收的输出变量的地址[IEnumRAWINPUTDEVICE](ienumrawinputdevice.md)接口指针。 如果该方法不成功，此输出变量的值未定义。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 HRESULT：此方法支持 E_INVALIDARG 和 e_outofmemory 等 E_UNEXPECTED 标准的返回值。  
  
## <a name="remarks"></a>备注  
 此方法可枚举序列中记录一个点，以便在以后返回到该点。 调用方必须释放此独立于第一个枚举器的新枚举器。
