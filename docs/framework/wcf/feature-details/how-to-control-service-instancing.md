---
title: 如何：控制服务实例化
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e0b12b34-8004-443a-a46d-83a5c00f2601
ms.openlocfilehash: 06324b30d2fbd68a12619375024b9f86019adbb1
ms.sourcegitcommit: af0a22a4eb11bbcd33baec49150d551955b50a16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56260956"
---
# <a name="how-to-control-service-instancing"></a>如何：控制服务实例化
通过设置服务的实例模式，可以指定创建 <xref:System.ServiceModel.InstanceContext?displayProperty=nameWithType>（及其关联的用户定义服务对象）的时间。 有关可能模式，请参见 <xref:System.ServiceModel.InstanceContextMode> 枚举。 有关行为的详细信息，请参阅[配置和扩展的运行时行为带有](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)。 有关工作示例，请参阅[行为](../../../../docs/framework/wcf/samples/behaviors.md)。  
  
### <a name="to-control-the-service-instance-lifetime-using-code"></a>使用代码控制服务实例生存期  
  
1.  将 <xref:System.ServiceModel.ServiceBehaviorAttribute> 应用于服务类。  
  
2.  将 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> 属性设置为下列值之一：<xref:System.ServiceModel.InstanceContextMode.PerCall>、<xref:System.ServiceModel.InstanceContextMode.PerSession> 或 <xref:System.ServiceModel.InstanceContextMode.Single>。  
  
     [!code-csharp[C_ControlServiceInstancing#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_controlserviceinstancing/cs/source.cs#1)]
     [!code-vb[C_ControlServiceInstancing#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_controlserviceinstancing/vb/source.vb#1)]  
  
## <a name="example"></a>示例  
 下面的代码示例将 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> 属性（attribute）的 <xref:System.ServiceModel.ServiceBehaviorAttribute> 属性（property）设置为 <xref:System.ServiceModel.InstanceContextMode.PerCall>。  
  
 [!code-csharp[c_ControlServiceInstancing#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_controlserviceinstancing/cs/source.cs#2)]
 [!code-vb[c_ControlServiceInstancing#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_controlserviceinstancing/vb/source.vb#2)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.ServiceModel.ServiceBehaviorAttribute>
- <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A>
- <xref:System.ServiceModel.InstanceContextMode>
- [服务：行为示例](../samples/behaviors.md)
