---
title: ICorDebug::CreateProcess 方法
ms.date: 03/30/2017
api_name:
- ICorDebug.CreateProcess
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebug::CreateProcess
helpviewer_keywords:
- ICorDebug::CreateProcess method [.NET Framework debugging]
- CreateProcess method, ICorDebugProcess interface [.NET Framework debugging]
ms.assetid: b6128694-11ed-46e7-bd4e-49ea1914c46a
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: cf7480eaa0fa38651d139a2fa9d533b43dbdce1b
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57496464"
---
# <a name="icordebugcreateprocess-method"></a>ICorDebug::CreateProcess 方法
启动进程和调试器的控制下其主线程。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT CreateProcess (  
    [in]  LPCWSTR                     lpApplicationName,  
    [in]  LPWSTR                      lpCommandLine,  
    [in]  LPSECURITY_ATTRIBUTES       lpProcessAttributes,  
    [in]  LPSECURITY_ATTRIBUTES       lpThreadAttributes,  
    [in]  BOOL                        bInheritHandles,  
    [in]  DWORD                       dwCreationFlags,  
    [in]  PVOID                       lpEnvironment,  
    [in]  LPCWSTR                     lpCurrentDirectory,  
    [in]  LPSTARTUPINFOW              lpStartupInfo,  
    [in]  LPPROCESS_INFORMATION       lpProcessInformation,  
    [in]  CorDebugCreateProcessFlags  debuggingFlags,  
    [out] ICorDebugProcess            **ppProcess  
);  
```  
  
## <a name="parameters"></a>参数  
 `lpApplicationName`  
 [in]指向一个以 null 结尾的字符串，指定要执行的启动进程的模块。 调用进程的安全上下文中执行模块。  
  
 `lpCommandLine`  
 [in]指定要执行的启动进程的命令行的以 null 结尾的字符串指针。 应用程序名称 (例如，"SomeApp.exe") 必须是第一个参数。  
  
 `lpProcessAttributes`  
 [in]指向 Win32`SECURITY_ATTRIBUTES`结构，它指定进程的安全描述符。 如果`lpProcessAttributes`是 null，则该过程获取的默认安全描述符。  
  
 `lpThreadAttributes`  
 [in]指向 Win32`SECURITY_ATTRIBUTES`结构，它指定进程的主线程的安全描述符。 如果`lpThreadAttributes`是 null，该线程将获取的默认安全描述符。  
  
 `bInheritHandles`  
 [in]设置为`true`以指示，在启动过程中，由继承调用进程中的每个可继承句柄或`false`以指示不会继承句柄。 继承的句柄具有相同值和访问权限，作为原始句柄。  
  
 `dwCreationFlags`  
 [in]按位组合[Win32 进程创建标志](https://go.microsoft.com/fwlink/?linkid=69981)用于控制优先级类和启动过程的行为。  
  
 `lpEnvironment`  
 [in]指向新的进程的环境块的指针。  
  
 `lpCurrentDirectory`  
 [in]指向一个以 null 结尾的字符串，指定进程的当前目录的完整路径。 如果此参数为 null，新进程将与调用进程具有相同的当前驱动器和目录。  
  
 `lpStartupInfo`  
 [in]指向 Win32`STARTUPINFOW`结构，它指定窗口区域、 桌面、 标准句柄和启动进程的主窗口的外观。  
  
 `lpProcessInformation`  
 [in]指向 Win32`PROCESS_INFORMATION`结构，它指定要启动的进程的标识信息。  
  
 `debuggingFlags`  
 [in]CorDebugCreateProcessFlags 枚举，指定调试选项的值。  
  
 `ppProcess`  
 [out]指向表示流程 ICorDebugProcess 对象的地址的指针。  
  
## <a name="remarks"></a>备注  
 此方法的参数都是相同的 Win32`CreateProcess`方法。  
  
 若要启用非托管混合模式调试，请设置`dwCreationFlags`DEBUG_PROCESS 到&#124;DEBUG_ONLY_THIS_PROCESS。 如果你想要使用仅托管调试，则不要设置这些标志。  
  
 如果调试器和过程来进行调试 （附加的进程） 共享单个控制台中，并使用互操作调试时，是否可以为附加的进程，以保存控制台锁并在调试事件处停止。 然后，调试器将阻止使用控制台的任何尝试。 若要避免此问题，在中设置 CREATE_NEW_CONSOLE 标志`dwCreationFlags`参数。  
  
 不支持 Win9x 和非 x86 平台，例如基于 IA-64 和 AMD64 基于平台进行互操作调试。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [ICorDebug 接口](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)
