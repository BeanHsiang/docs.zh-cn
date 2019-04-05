---
title: StrongNameSignatureGenerationEx 函数
ms.date: 03/30/2017
api_name:
- StrongNameSignatureGenerationEx
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- StrongNameSignatureGenerationEx
helpviewer_keywords:
- StrongNameSignatureGenerationEx function [.NET Framework strong naming]
ms.assetid: 9a75469e-aa49-4e32-ad48-3bafd5202f09
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c63a586473128281843ec100905e63d381f1a3f7
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57500925"
---
# <a name="strongnamesignaturegenerationex-function"></a>StrongNameSignatureGenerationEx 函数
为指定的程序集，根据指定的标志生成的强名称签名。  
  
 此函数已弃用。 使用[iclrstrongname:: Strongnamesignaturegenerationex](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamesignaturegenerationex-method.md)方法相反。  
  
## <a name="syntax"></a>语法  
  
```  
BOOLEAN StrongNameSignatureGenerationEx (  
    [in]  LPCWSTR   wszFilePath,  
    [in]  LPCWSTR   wszKeyContainer,  
    [in]  BYTE      *pbKeyBlob,  
    [in]  ULONG     cbKeyBlob,  
    [out] BYTE      **ppbSignatureBlob,  
    [out] ULONG     *pcbSignatureBlob,  
    [in]  DWORD     dwFlags  
);  
```  
  
## <a name="parameters"></a>参数  
 `wszFilePath`  
 [in]包含为其生成强名称签名的程序集的清单文件的路径。  
  
 `wszKeyContainer`  
 [in]包含公钥/私钥对的密钥容器的名称。  
  
 如果`pbKeyBlob`为 null，`wszKeyContainer`必须指定加密服务提供商 (CSP) 内有效的容器。 在这种情况下，使用容器中存储的密钥对文件进行签名。  
  
 如果`pbKeyBlob`不为 null，则假定为密钥对要包含在密钥二进制大型对象 (BLOB) 中。  
  
 `pbKeyBlob`  
 [in]一个指向公钥/私钥对。 此对的格式创建的 Win32`CryptExportKey`函数。 如果`pbKeyBlob`是 null，指定的密钥容器`wszKeyContainer`假定包含密钥对。  
  
 `cbKeyBlob`  
 [in]大小，以字节为单位的`pbKeyBlob`。  
  
 `ppbSignatureBlob`  
 [out]指向该签名返回到公共语言运行时的位置的指针。 如果`ppbSignatureBlob`是 null，则运行时存储签名中指定的文件`wszFilePath`。  
  
 如果`ppbSignatureBlob`是不为 null，公共语言运行时分配用于返回签名的空间。 调用方必须释放此空间使用[StrongNameFreeBuffer](../../../../docs/framework/unmanaged-api/strong-naming/strongnamefreebuffer-function.md)函数。  
  
 `pcbSignatureBlob`  
 [out]以字节为单位，返回的签名的大小。  
  
 `dwFlags`  
 [in]一个或多个以下值：  
  
-   `SN_SIGN_ALL_FILES` (0x00000001) 的重新计算链接的模块的所有哈希值。  
  
-   `SN_TEST_SIGN` (0x00000002) — 测试签名程序集。  
  
## <a name="return-value"></a>返回值  
 `true` 在成功完成;否则为`false`。  
  
## <a name="remarks"></a>备注  
 指定为 null`wszFilePath`来计算而无需创建签名的签名的大小。  
  
 可直接在文件中，存储或返回给调用方签名。  
  
 如果`SN_SIGN_ALL_FILES`指定但尚未包含的公共密钥 (同时`pbKeyBlob`和`wszFilePath`均为 null)，重新计算链接的模块的哈希值，但不重新签名程序集。  
  
 如果`SN_TEST_SIGN`指定，则公共语言运行时标头尚未修改以指示该程序集具有强名称签名。  
  
 如果`StrongNameSignatureGenerationEx`函数不成功完成，则调用[StrongNameErrorInfo](../../../../docs/framework/unmanaged-api/strong-naming/strongnameerrorinfo-function.md)函数检索最后一个生成的错误。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** StrongName.h  
  
 **库：** 包含为 MsCorEE.dll 中的资源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [StrongNameSignatureGenerationEx 方法](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamesignaturegenerationex-method.md)
- [StrongNameSignatureGeneration 方法](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamesignaturegeneration-method.md)
- [ICLRStrongName 接口](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-interface.md)
