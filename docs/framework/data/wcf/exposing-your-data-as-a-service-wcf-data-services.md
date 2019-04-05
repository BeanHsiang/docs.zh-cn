---
title: 将数据公开为服务（WCF 数据服务）
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, configuring
- getting started, WCF Data Services
- WCF Data Services, getting started
ms.assetid: df0bbcee-f66f-4a88-abb4-4e73c8b9c908
ms.openlocfilehash: 8e598dde0d85b1d7d4208bf2475a0f6f6eee34a6
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54700983"
---
# <a name="expose-your-data-as-a-service-wcf-data-services"></a>将数据公开为服务 (WCF Data Services)

WCF Data Services 与 Visual Studio，以便你可以更轻松地定义用于公开为数据服务集成[!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)]馈送。 创建公开 OData 源的数据服务涉及以下基本步骤：

1.  **定义数据模型。** WCF 数据服务本身支持基于的数据模型[ADO.NET 实体框架](../../../../docs/framework/data/adonet/ef/index.md)。 有关详细信息，请参阅[如何：创建数据服务使用 ADO.NET 实体框架数据源](../../../../docs/framework/data/wcf/create-a-data-service-using-an-adonet-ef-data-wcf.md)。

     WCF 数据服务还支持基于返回的实例的公共语言运行时 (CLR) 对象的数据模型<xref:System.Linq.IQueryable%601>接口。 通过此功能，您可以在 .NET Framework 中部署基于列表、数组和集合的数据服务。 若要启用针对这些数据结构的创建、更新和删除操作，还必须实现 <xref:System.Data.Services.IUpdatable> 接口。 有关详细信息，请参阅[如何：创建数据服务使用反射提供程序](../../../../docs/framework/data/wcf/create-a-data-service-using-rp-wcf-data-services.md)。

     对于更高级的方案，WCF Data Services 包括一组使您可以定义基于后期绑定数据类型的数据模型的提供程序。 有关详细信息，请参阅[自定义数据服务提供商](../../../../docs/framework/data/wcf/custom-data-service-providers-wcf-data-services.md)。

2.  **创建数据服务。** 大多数基本数据服务公开一个从 <xref:System.Data.Services.DataService%601> 类继承的类和一个作为实体容器的命名空间限定名称的 `T` 类型。 有关详细信息，请参阅 [Defining WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)的信息。

3.  **配置数据服务。** 默认情况下，WCF 数据服务禁用对由实体容器公开的资源的访问。 <xref:System.Data.Services.DataServiceConfiguration>接口，您可以配置对资源的访问和服务操作，指定受支持的版本的 OData，并定义其他服务范围的行为，例如批处理行为或最大可返回的实体数如果单个响应。 有关详细信息，请参阅[数据服务配置](../../../../docs/framework/data/wcf/configuring-the-data-service-wcf-data-services.md)。

有关如何创建基于 Northwind 示例数据库的简单数据服务的示例，请参阅[快速入门](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)。

## <a name="see-also"></a>请参阅

- [入门](../../../../docs/framework/data/wcf/getting-started-with-wcf-data-services.md)
- [概述](../../../../docs/framework/data/wcf/wcf-data-services-overview.md)