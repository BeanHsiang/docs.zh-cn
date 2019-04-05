---
title: StrongNameKeyInstall 函数
ms.date: 03/30/2017
api_name:
- StrongNameKeyInstall
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- StrongNameKeyInstall
helpviewer_keywords:
- StrongNameKeyInstall function [.NET Framework strong naming]
ms.assetid: e32fd546-7757-4681-be3d-658e93281e50
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6b3fc69b2edf611383402b13555cf33be10dbad3
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57366577"
---
# <a name="strongnamekeyinstall-function"></a>StrongNameKeyInstall 函数

将公钥/私钥对导入容器。

此函数已弃用。 使用[iclrstrongname:: Strongnamekeyinstall](../hosting/iclrstrongname-strongnamekeyinstall-method.md)方法相反。

## <a name="syntax"></a>语法

```cpp
BOOLEAN StrongNameKeyInstall (
    [in]  LPCWSTR   wszKeyContainer,
    [in]  BYTE      *pbKeyBlob,
    [in]  ULONG     cbKeyBlob
);
```

## <a name="parameters"></a>参数

`wszKeyContainer`\
[in]密钥容器的名称。 `wszKeyContainer` 必须为非空字符串。

`pbKeyBlob`\
[in]二进制密钥对。

`cbKeyBlob`\
[in]大小，以字节为单位的`pbKeyBlob`。

## <a name="return-value"></a>返回值

`true` 在成功完成;否则为`false`。

## <a name="remarks"></a>备注

使用[StrongNameKeyDelete](strongnamekeydelete-function.md)函数来删除密钥容器。

如果`StrongNameKeyInstall`函数不成功完成，则调用[StrongNameErrorInfo](strongnameerrorinfo-function.md)函数检索最后一个生成的错误。

## <a name="requirements"></a>要求

**平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。

**标头：** StrongName.h

**库：** 包含为 MsCorEE.dll 中的资源

**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]

## <a name="see-also"></a>请参阅

- [StrongNameKeyInstall 方法](../hosting/iclrstrongname-strongnamekeyinstall-method.md)
- [StrongNameKeyDelete 方法](../hosting/iclrstrongname-strongnamekeydelete-method.md)
- [ICLRStrongName 接口](../hosting/iclrstrongname-interface.md)