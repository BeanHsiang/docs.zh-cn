---
title: 如何：为应用程序设置默认基于时间的缓存策略
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time-based cache policies
- cache [.NET Framework], time-based policies
- default time-based cache policy
ms.assetid: 6bfce066-a2e7-4add-a05e-85c12ec9f07f
ms.openlocfilehash: d40b0ffbe514429ed24eaa5d0c2ce2d52c80d37d
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54608948"
---
# <a name="how-to-set-the-default-time-based-cache-policy-for-an-application"></a>如何：为应用程序设置默认基于时间的缓存策略
默认基于时间的缓存策略允许应用程序将标头定义的缓存行为与缓存资源和 RFC 2616 的第 13 和 14 节（可在 [工程任务组 (IETF)](https://www.ietf.org/) 中找到）中定义的缓存行为一起发送。 这是适用于大多数应用程序的缓存行为。  
  
### <a name="to-set-the-default-automatic-policy-for-an-application"></a>为应用程序设置默认自动策略  
  
1.  创建默认基于时间的策略对象。  
  
2.  将策略对象设置为应用程序域的默认对象。  
  
## <a name="example"></a>示例  
 此部分中的两个示例生成相同的策略。  
  
 以下示例创建默认基于时间的策略，并为应用程序域将其设置为默认。  
  
```csharp  
public static void SetDefaultTimeBasedPolicy ()  
{  
    HttpRequestCachePolicy policy = new HttpRequestCachePolicy ();  
    HttpWebRequest.DefaultCachePolicy = policy ;  
}  
```  
  
```vb  
Public Shared Sub SetDefaultTimeBasedPolicy ()  
    Dim policy = New HttpRequestCachePolicy ()  
    HttpWebRequest.DefaultCachePolicy = policy  
End Sub  
```  
  
 也可使用 <xref:System.Net.Cache.RequestCachePolicy> 类创建默认基于时间的缓存策略，如以下示例所示：  
  
```csharp  
public static void SetDefaultTimeBasedPolicy2()  
{  
    RequestCachePolicy policy = new RequestCachePolicy ();  
    HttpWebRequest.DefaultCachePolicy = policy ;  
}  
```  
  
```vb  
Public Shared Sub SetDefaultTimeBasedPolicy2()  
    Dim policy As New RequestCachePolicy()  
    HttpWebRequest.DefaultCachePolicy = policy  
End Sub  
```  
  
## <a name="see-also"></a>请参阅
- [网络应用程序的缓存管理](../../../docs/framework/network-programming/cache-management-for-network-applications.md)
- [缓存策略](../../../docs/framework/network-programming/cache-policy.md)
- [基于位置的缓存策略](../../../docs/framework/network-programming/location-based-cache-policies.md)
- [基于时间的缓存策略](../../../docs/framework/network-programming/time-based-cache-policies.md)
- [\<requestCaching> 元素（网络设置）](../../../docs/framework/configure-apps/file-schema/network/requestcaching-element-network-settings.md)
