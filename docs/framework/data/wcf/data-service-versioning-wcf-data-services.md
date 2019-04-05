---
title: 数据服务版本管理（WCF 数据服务）
ms.date: 03/30/2017
helpviewer_keywords:
- versioning, WCF Data Services
- versioning [WCF Data Services]
- WCF Data Services, versioning
ms.assetid: e3e899cc-7f25-4f67-958f-063f01f79766
ms.openlocfilehash: 818495cd2f7100f416280ce019321fed3f26aee8
ms.sourcegitcommit: d2ccb199ae6bc5787b4762e9ea6d3f6fe88677af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56092912"
---
# <a name="data-service-versioning-wcf-data-services"></a>数据服务版本管理（WCF 数据服务）
[!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] ，可创建数据服务，以便客户端可以作为基于数据模型的资源使用 Uri 访问数据。 OData 还支持服务操作的定义。 这些数据服务在初始部署之后，可能出于多种原因（例如，更改业务需求、信息技术需求，或者为了解决其他问题）而需要更改，并且在其生存期期间可能需要更改多次。 更改现有数据服务时，您必须考虑是否要定义您的数据服务的新版本以及如何将对现有客户端应用程序的影响降至最低。 本主题提供了有关何时以及如何创建一个新版本的数据服务的指导。 它还介绍了 WCF 数据服务如何处理客户端和数据服务支持 OData 协议的不同版本之间的交换。

## <a name="versioning-a-wcf-data-service"></a>WCF 数据服务版本管理
 一旦部署数据服务和使用数据，对数据服务的更改有可能导致与现有客户端应用程序的兼容性问题。 但是，因为服务的整体业务需求而经常需要进行更改，您必须考虑何时以及如何创建一个新的数据服务版本，以最大程度减小对客户端上应用程序的影响。

### <a name="data-model-changes-that-recommend-a-new-data-service-version"></a>建议发布新的数据服务版本的数据模型更改
 在考虑是否要发布数据服务的新版本时，了解不同种类的更改如何影响客户端应用程序很重要。 可能要求您创建一个新版本的数据服务的数据服务更改可分为以下两个类别：

-   对服务协定的更改 — 它包括对服务操作的更新、对实体集（源）的可访问性的更改或对服务行为的其他更改。

-   对数据协定的更改 — 它包括对数据模型、源格式或源自定义的更改。

 下表详细说明出现哪类更改时您应考虑发布新版本的数据服务：

|更改类型|需要新版本|不需要新版本|
|--------------------|----------------------------|----------------------------|
|服务操作|-添加新的参数<br />更改返回类型<br />-删除服务操作|-删除现有参数<br />-添加新的服务操作|
|服务行为|-禁用计数请求<br />-禁用投影支持<br />-增加所需的数据服务版本|-启用计数请求<br />-启用投影支持<br />-减少所需的数据服务版本|
|实体集权限|-限制实体集权限<br />-更改响应代码 (新第一个数字值) <sup>1</sup>|-放宽实体集权限<br />-更改响应代码 (相同第一个数字值)|
|实体属性|-删除现有属性或关系<br />添加不可为 null 的属性<br />-更改现有属性|添加可为 null 属性<sup>2</sup>|
|实体集|-删除实体集|添加派生的类型<br />-将基类型<br />添加实体集|
|源自定义|更改实体属性映射||

 <sup>1</sup>这可能取决于客户端应用程序依赖于接收的特定错误代码的严格程度。

 <sup>2</sup>可以设置<xref:System.Data.Services.Client.DataServiceContext.IgnoreMissingProperties%2A>属性设置为`true`让客户端忽略数据服务发送的客户端未定义任何新属性。 但是，当插入时，客户端在 POST 请求中不包括的属性都设置为其默认值。 对于更新，对客户端未知的属性中任何现有数据可能用默认值改写。 在此情况下，应将更新作为 MERGE 要求发送，这是默认值。 有关详细信息，请参阅[管理数据服务上下文](../../../../docs/framework/data/wcf/managing-the-data-service-context-wcf-data-services.md)。

### <a name="how-to-version-a-data-service"></a>如何对数据服务进行版本管理
 在需要时，通过创建新服务实例（使用更新的服务协定或数据模型）定义新的数据服务版本。 通过使用新的 URI 终结点（使其与以前的版本不同）公开该新服务。 例如：

-   旧版本：`http://services.odata.org/Northwind/v1/Northwind.svc/`

-   新版本：`http://services.odata.org/Northwind/v2/Northwind.svc/`

 升级数据服务时，客户端将需要也更新（基于新的数据服务的元数据）并使用新的根 URI。 如果可能，您应维护以前版本的数据服务以支持尚未升级、无法使用新版本的客户端。 在不再需要时，可以删除旧版本的数据服务。 您应该考虑在外部配置文件中维护数据服务终结点 URI。

## <a name="odata-protocol-versions"></a>OData 协议版本
 OData 的新版本的发布，客户端应用程序可能不使用相同版本的数据服务支持 OData 协议。 较旧的客户端应用程序可能会访问数据服务支持 OData 的较新版本。 客户端应用程序也可能使用 WCF 数据服务客户端库，该库支持 OData 的较新版本，比正在访问的数据服务的较新版本。

 WCF 数据服务将利用 OData 来处理此类版本控制方案提供的支持。 此外，还有支持生成和使用数据模型元数据创建客户端数据服务类时客户端使用的版本不同的 OData 数据服务使用。 有关详细信息，请参阅[OData:协议版本控制](https://go.microsoft.com/fwlink/?LinkId=186071)。

### <a name="version-negotiation"></a>版本协商
 数据服务可以配置为定义的服务，而不考虑客户端请求的版本将使用 OData 协议的最高版本。 您可以执行此操作通过指定<xref:System.Data.Services.Common.DataServiceProtocolVersion>值<xref:System.Data.Services.DataServiceBehavior.MaxProtocolVersion%2A>属性的<xref:System.Data.Services.DataServiceBehavior>由数据服务。 有关详细信息，请参阅[数据服务配置](../../../../docs/framework/data/wcf/configuring-the-data-service-wcf-data-services.md)。

 当应用程序使用 WCF 数据服务客户端库来访问数据服务时，库自动设置这些标头为正确的值，具体取决于 OData 和应用程序中使用的功能的版本。 默认情况下，WCF 数据服务使用支持请求的操作的最低协议版本。

 下表详细介绍的版本[!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]和[!INCLUDE[silverlight](../../../../includes/silverlight-md.md)]，包括对特定版本的 OData 协议的 WCF 数据服务支持。

|OData 协议版本|支持引入方式|
|-----------------------------------------------------------------------------------|----------------------------|
|1 版|-   [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] Service Pack 1 (SP1)<br />-   [!INCLUDE[silverlight](../../../../includes/silverlight-md.md)] 版本 3|
|2 版|-   [!INCLUDE[netfx40_long](../../../../includes/netfx40-long-md.md)]<br />-对更新[!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)]SP1。 您可以下载和安装从更新[Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkId=158125)。<br />-   [!INCLUDE[silverlight](../../../../includes/silverlight-md.md)] 版本 4|
|3 版|-你可以下载并安装支持从 OData 版本 3 的预发行版本[Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkId=203885)。|

### <a name="metadata-versions"></a>元数据版本
 默认情况下，WCF 数据服务使用 1.1 版的 CSDL 表示数据模型。 对于基于反射提供程序或自定义数据服务提供程序的数据模型始终如此。 但是，如果数据模型是使用[!INCLUDE[adonet_ef](../../../../includes/adonet-ef-md.md)]定义的，则返回的 CSDL 版本就是该[!INCLUDE[adonet_ef](../../../../includes/adonet-ef-md.md)]所用的版本。 CSDL 的版本由的命名空间[架构元素 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#schema-element-csdl)。

 返回的元数据的 `DataServices` 元素还包含一个 `DataServiceVersion` 特性，该特性的值与响应消息中 `DataServiceVersion` 标头的值相同。 客户端应用程序，如**添加服务引用**对话框在 Visual Studio 中，使用此信息来生成正确使用承载数据服务的 WCF 数据服务的版本的客户端数据服务类。 有关详细信息，请参阅[OData:协议版本控制](https://go.microsoft.com/fwlink/?LinkId=186071)。

## <a name="see-also"></a>请参阅

- [数据服务提供程序](../../../../docs/framework/data/wcf/data-services-providers-wcf-data-services.md)
- [定义 WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)
