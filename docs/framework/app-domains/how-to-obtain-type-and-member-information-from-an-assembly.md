---
title: 如何：从程序集获得类型和成员信息
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- obtaining assembly information
- assemblies [.NET Framework], obtaining information from
ms.assetid: 348ae651-ccda-4f13-8eda-19e8337e9438
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ef3fbb7af3097a67cb39f0c3b2ee294b86f0600e
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54701594"
---
# <a name="how-to-obtain-type-and-member-information-from-an-assembly"></a>如何：从程序集获得类型和成员信息
<xref:System.Reflection> 命名空间包含许多从程序集中获取信息的方法。 本部分介绍其中的一种方法。 有关其他信息，请参阅[反射概述](../../../docs/framework/reflection-and-codedom/reflection.md)。  
  
 下例演示从程序集获取类型和成员信息。  
  
## <a name="example"></a>示例  
 [!code-cpp[Conceptual.Types.ViewInfo#8](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.types.viewinfo/cpp/source6.cpp#8)]
 [!code-csharp[Conceptual.Types.ViewInfo#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.types.viewinfo/cs/source6.cs#8)]
 [!code-vb[Conceptual.Types.ViewInfo#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.types.viewinfo/vb/source6.vb#8)]  
  
## <a name="see-also"></a>请参阅
- [对应用程序域进行编程](./application-domains.md#programming-with-application-domains)
- [反射](../../../docs/framework/reflection-and-codedom/reflection.md)
- [使用应用程序域](../../../docs/framework/app-domains/use.md)
