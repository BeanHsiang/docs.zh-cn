---
title: 配置加密类
ms.date: 03/30/2017
helpviewer_keywords:
- configuration files [.NET Framework], cryptography
- cryptographic algorithms
- security [.NET Framework], encryption
- cryptography, classes
- .NET Framework application configuration, cryptography
- default cryptography
ms.assetid: eee3ccb8-2c0d-4f35-b38d-6892a46c14e5
ms.openlocfilehash: ba11eed316e227ceae4cb5acecb2b081fa8868f2
ms.sourcegitcommit: b351b0781a035616c90c68ccae6dd60aae66a953
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2019
ms.locfileid: "55084401"
---
# <a name="configuring-cryptography-classes"></a>配置加密类
[!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)]允许计算机管理员配置的默认加密算法和.NET Framework 和相应地编写的应用程序使用的算法实现。  例如，具有其自己的加密算法的实现的企业可以使该实现而不是实现中提供默认[!INCLUDE[winsdkshort](../../../includes/winsdkshort-md.md)]。 尽管使用加密的托管应用程序始终可以选择显式绑定到特定的实现，但建议他们使用的加密配置系统创建加密对象。  
  
## <a name="in-this-section"></a>本节内容  
 [将算法名称映射到加密类](../../../docs/framework/configure-apps/map-algorithm-names-to-cryptography-classes.md)  
 介绍如何将算法名称映射到加密类。  
  
 [将对象标识符映射到加密算法](../../../docs/framework/configure-apps/map-object-identifiers-to-cryptography-algorithms.md)  
 介绍如何将对象标识符映射到加密算法。  
  
## <a name="related-sections"></a>相关章节  
 [Cryptographic Services](../../../docs/standard/security/cryptographic-services.md)  
 提供的加密服务提供的概述[!INCLUDE[winsdkshort](../../../includes/winsdkshort-md.md)]。  
  
 [加密设置架构](../../../docs/framework/configure-apps/file-schema/cryptography/index.md)  
 描述将友好算法名映射到实现密码算法的类的元素。
