---
title: 部署注意事项（实体框架）
ms.date: 03/30/2017
ms.assetid: 3a847a22-4eb8-4565-b18b-453bbca070db
ms.openlocfilehash: 683f5e9b43bceb09d6354079fd9f7fcb7ed09eac
ms.sourcegitcommit: 3500c4845f96a91a438a02ef2c6b4eef45a5e2af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/07/2019
ms.locfileid: "55828080"
---
# <a name="deployment-considerations-entity-framework"></a>部署注意事项（实体框架）
本主题提供有关部署使用 ADO.NET 实体框架进行数据访问的应用程序的信息。 有关实体框架的详细信息，请参阅[Getting Started](../../../../../docs/framework/data/adonet/ef/getting-started.md)。  
  
 实体框架提供了一组与 Visual Studio 集成的工具，使得在 Visual Studio 中进行开发更加容易。 有关详细信息，请参阅[ADO.NET 实体数据模型工具](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399249(v=vs.100))。 本主题未介绍如何使用特定技术部署基于实体框架的应用程序。  
  
 Visual Studio 提供用于分发和部署应用程序的工具（例如 ClickOnce 部署）。 有关详细信息，请参阅[部署应用程序和组件](/visualstudio/deployment/deploying-applications-services-and-components)Visual Studio 文档中。  
  
 部署使用实体框架的应用程序时需要考虑以下注意事项：  
  
-   自 .NET Framework 3.5 Service Pack 1 (SP1) 起实体框架成为 .NET Framework 的一个组件。 部署基于 Entity Framework 的应用程序时必须确保安装了 .NET Framework 3.5 SP1 或更高版本。  
  
-   当概念模型由实体数据模型向导生成时，将在应用程序配置文件中创建连接字符串。 模型和映射文件可以作为应用程序资源嵌入，或复制到输出目录中。 默认情况下，它们部署为嵌入的应用程序资源。 使用实体设计器文件的 `Metadata Artifact Processing` 属性可选择这些选项之一。 有关详细信息，请参阅[如何：复制模型并将文件映射到输出目录](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc716709(v=vs.100))。  
  
-   确保模型和映射信息（以概念架构定义语言 (CSDL)、存储架构定义语言 (SSDL) 和映射规范语言 (MSL) 表示）与应用程序一起部署在由连接字符串指定的位置。 有关详细信息，请参阅[连接字符串](../../../../../docs/framework/data/adonet/ef/connection-strings.md)。  
  
-   在将模型和映射信息作为应用程序资源嵌入时，每次更新概念模型时，都必须重新编译和重新部署应用程序。  
  
-   因为实体框架是 .NET Framework 的一个组件，因此在 .NET Framework 许可协议许可的情况下可以与您的应用程序一起重新分发该组件。  
  
## <a name="see-also"></a>请参阅
- [ADO.NET 实体框架](../../../../../docs/framework/data/adonet/ef/index.md)
- [开发和部署注意事项](../../../../../docs/framework/data/adonet/ef/development-and-deployment-considerations.md)
