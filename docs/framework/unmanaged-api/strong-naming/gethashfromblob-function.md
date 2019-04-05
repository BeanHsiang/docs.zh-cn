---
title: GetHashFromBlob 函数
ms.date: 03/30/2017
api_name:
- GetHashFromBlob
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- GetHashFromBlob
helpviewer_keywords:
- GetHashFromBlob function [.NET Framework strong naming]
ms.assetid: b712d862-f2d0-4b55-87d4-65bbeadef982
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3d9e7b52c9061a1a7b470f9d4abf735e605087dc
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57352069"
---
# <a name="gethashfromblob-function"></a>GetHashFromBlob 函数

使用指定的哈希算法获取指定内存地址处的程序集的哈希。

此函数已弃用。 使用[iclrstrongname:: Gethashfromblob](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-gethashfromblob-method.md)方法相反。

## <a name="syntax"></a>语法

```cpp
HRESULT GetHashFromBlob (
    [in]  BYTE    *pbBlob,
    [in]  DWORD   cchBlob,
    [in, out] unsigned int   *piHashAlg,
    [out] BYTE    *pbHash,
    [in]  DWORD   cchHash,
    [out] DWORD   *pchHash
);
```

## <a name="parameters"></a>参数

`pbBlob`\
[in]指向要进行哈希处理的内存块的地址的指针。

`cchBlob`\
[in]内存块的长度，以字节为单位。

`piHashAlg`\
[in、 out]一个常量，它指定哈希算法。 使用默认的算法为零。

`pbHash`\
[out]返回的哈希缓冲区中。

`cchHash`\
[in]请求的最大大小的`pbHash`。

`pchHash`\
[out]大小 （字节），则返回的`pbHash`。

## <a name="requirements"></a>要求

**平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。

**标头：** StrongName.h

**库：** 包含为 MsCorEE.dll 中的资源

**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]

## <a name="see-also"></a>请参阅

- [GetHashFromBlob 方法](../hosting/iclrstrongname-gethashfromblob-method.md)
- [ICLRStrongName 接口](../hosting/iclrstrongname-interface.md)