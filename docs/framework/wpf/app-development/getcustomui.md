---
title: GetCustomUI
ms.date: 03/30/2017
helpviewer_keywords:
- custom error messages [WPF]
ms.assetid: e55180fc-35bb-4f80-a136-772b5eb3e4e5
ms.openlocfilehash: af51a0d76ac080017f58ac8fc3acca86c23fb480
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57474860"
---
# <a name="getcustomui"></a>GetCustomUI
如果实现由 PresentationHost.exe 从主机获取自定义进度和错误消息调用。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT GetCustomUI( [out] BSTR* pwzProgressAssemblyName, [out] BSTR* pwzProgressClassName, [out] BSTR* pwzErrorAssemblyName, [out] BSTR* pwzErrorClassName );  
```  
  
## <a name="parameters"></a>参数  
 `pwzProgressAssemblyName`  
  
 [out]指向包含主机提供进度用户界面的程序集的指针。  
  
 `pwzProgressClassName`  
  
 [out]最好是为主机提供进度用户界面，类的名称[!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)]文件具有<xref:System.Windows.Controls.Page>是其顶级元素。 此类驻留在由指定的程序集`pwzProgressAssemblyName`。  
  
 `pwzErrorAssemblyName`  
  
 [out]指向包含主机提供的错误用户界面的程序集的指针。  
  
 `pwzErrorClassName`  
  
 [out]为主机提供的错误用户类的名称最好是接口具有的 XAML 文件<xref:System.Windows.Controls.Page>是其顶级元素。 此类驻留在由指定的程序集`pwzErrorAssemblyName`。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 HRESULT：已忽略。  
  
## <a name="remarks"></a>备注  
 主机应用程序可能具有可能不符合 PresentationHost.exe 的默认用户界面的特定主题。 如果是这样，主机应用程序可以实现[GetCustomUI](getcustomui.md)返回进度和错误的用户界面到 PresentationHost.exe。 将始终调用 PresentationHost.exe [GetCustomUI](getcustomui.md)之前使用其默认用户界面。  
  
 一次在 PresentationHost 的初始化期间调用此函数。  
  
## <a name="see-also"></a>请参阅
- [IWpfHostSupport](iwpfhostsupport.md)
