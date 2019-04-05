---
title: CorMethodAttr 枚举
ms.date: 03/30/2017
api_name:
- CorMethodAttr
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorMethodAttr
helpviewer_keywords:
- CorMethodAttr enumeration [.NET Framework metadata]
ms.assetid: 4e0c3521-e54d-43c1-9857-cc76b49b8ffc
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 1a69ca889e226168adb1b84ab64dc0f882c27606
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54520524"
---
# <a name="cormethodattr-enumeration"></a>CorMethodAttr 枚举
包含描述一种方法的功能的值。  
  
## <a name="syntax"></a>语法  
  
```  
typedef enum CorMethodAttr {  
  
    mdMemberAccessMask          =   0x0007,  
    mdPrivateScope              =   0x0000,  
    mdPrivate                   =   0x0001,  
    mdFamANDAssem               =   0x0002,  
    mdAssem                     =   0x0003,  
    mdFamily                    =   0x0004,  
    mdFamORAssem                =   0x0005,  
    mdPublic                    =   0x0006,  
  
    mdStatic                    =   0x0010,  
    mdFinal                     =   0x0020,  
    mdVirtual                   =   0x0040,  
    mdHideBySig                 =   0x0080,  
  
    mdVtableLayoutMask          =   0x0100,  
    mdReuseSlot                 =   0x0000,  
    mdNewSlot                   =   0x0100,  
  
    mdCheckAccessOnOverride     =   0x0200,  
    mdAbstract                  =   0x0400,  
    mdSpecialName               =   0x0800,  
  
    mdPinvokeImpl               =   0x2000,  
    mdUnmanagedExport           =   0x0008,  
  
    mdReservedMask              =   0xd000,  
    mdRTSpecialName             =   0x1000,  
    mdHasSecurity               =   0x4000,  
    mdRequireSecObject          =   0x8000,  
  
} CorMethodAttr;  
```  
  
## <a name="members"></a>成员  
  
|成员|描述|  
|------------|-----------------|  
|`mdMemberAccessMask`|指定成员访问权限。|  
|`mdPrivateScope`|指定该成员不能被引用。|  
|`mdPrivate`|指定该成员是只能由父类型访问。|  
|`mdFamANDAssem`|指定该成员是仅在此程序集中的子类型访问。|  
|`mdAssem`|指定该成员是可访问的程序集中的任何人。|  
|`mdFamily`|指定该成员是只能由类型和子类型访问。|  
|`mdFamORAssem`|指定该成员是可由派生类中它的程序集的其他类型访问。|  
|`mdPublic`|指定该成员是由下列所有类型与访问作用域可访问。|  
|`mdStatic`|指定为该类型的一部分而不是实例成员定义成员。|  
|`mdFinal`|指定不能重写该方法。|  
|`mdVirtual`|指定可以重写该方法。|  
|`mdHideBySig`|指定的方法按名称和签名，而不是只按名称隐藏。|  
|`mdVtableLayoutMask`|指定虚拟表布局。|  
|`mdReuseSlot`|指定用于此方法在虚拟表中的槽在重用。 这是默认设置。|  
|`mdNewSlot`|指定此方法总是获取虚拟表中的新槽。|  
|`mdCheckAccessOnOverride`|指定可以通过向其是可见的相同类型中重写该方法。|  
|`mdAbstract`|指定未实现方法。|  
|`mdSpecialName`|指定的方法是特殊字符，其名称描述如何。|  
|`mdPinvokeImpl`|指定使用 PInvoke 转发该方法的实现。|  
|`mdUnmanagedExport`|指定的方法是导出到非托管代码的托管的方法。|  
|`mdReservedMask`|公共语言运行时，保留供内部使用。|  
|`mdRTSpecialName`|指定公共语言运行时应检查的方法名称的编码。|  
|`mdHasSecurity`|指定该方法具有与之关联的安全。|  
|`mdRequireSecObject`|指定该方法调用包含安全代码的另一种方法。|  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorHdr.h  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [Metadata 枚举](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
