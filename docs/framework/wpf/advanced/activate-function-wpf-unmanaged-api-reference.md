---
title: 激活函数 （WPF 非托管 API 参考）
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- Activate
api_location:
- PresentationHost_v0400.dll
ms.assetid: 1400329c-b598-465f-80f2-e3dabf044811
ms.openlocfilehash: ee231653815bd5ef75d58979034e3b3be9f5ba54
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57480775"
---
# <a name="activate-function-wpf-unmanaged-api-reference"></a>激活函数 （WPF 非托管 API 参考）

此 API 支持 Windows Presentation Foundation (WPF) 基础结构，不应在代码中直接使用。

Windows Presentation Foundation (WPF) 基础结构使用的 windows 管理。

## <a name="syntax"></a>语法

```cpp
void Activate(
    const ActivateParameters* pParameters,
    __deref_out_ecount(1) LPUNKNOWN* ppInner,
    );
```

## <a name="parameters"></a>参数

`pParameters`\
指向窗口的激活参数的指针。

`ppInner`\
指向包含一个指向单个元素缓冲区的地址的指针<xref:Microsoft.VisualStudio.OLE.Interop.IOleDocument>对象。

## <a name="requirements"></a>要求

**平台：** 请参阅[.NET Framework 系统需求](../../get-started/system-requirements.md)。

**DLL:**

在.NET Framework 3.0 和 3.5:PresentationHostDLL.dll

在.NET Framework 4 及更高版本：PresentationHost_v0400.dll

**.NET framework 版本：** [!INCLUDE[net_current_v30plus](../../../../includes/net-current-v30plus-md.md)]

## <a name="see-also"></a>请参阅

- [WPF 非托管 API 参考](wpf-unmanaged-api-reference.md)
