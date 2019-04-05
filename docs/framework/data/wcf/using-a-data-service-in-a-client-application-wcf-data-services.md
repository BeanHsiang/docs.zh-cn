---
title: 在客户端应用程序中使用数据服务（WCF 数据服务）
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, client library
- WCF Data Services, getting started
ms.assetid: 90872d0c-e989-4490-b3e9-54afb10d33d4
ms.openlocfilehash: ff68a8bee17b55f7865d6f6c289ba514729be70d
ms.sourcegitcommit: d2ccb199ae6bc5787b4762e9ea6d3f6fe88677af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56093433"
---
# <a name="using-a-data-service-in-a-client-application-wcf-data-services"></a>在客户端应用程序中使用数据服务（WCF 数据服务）
您可以访问公开的服务[!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)]源向 Web 浏览器提供 URI。 URI 提供某个资源的地址，系统将向这些地址发送请求消息以访问或更改该资源表示的基础数据。 浏览器发出 HTTP GET 命令，并以 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源的形式返回请求的资源。 有关详细信息，请参阅[从 Web 浏览器访问服务](../../../../docs/framework/data/wcf/accessing-the-service-from-a-web-browser-wcf-data-services-quickstart.md)。  
  
 尽管可以使用 Web 浏览器测试 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 服务能否返回预期的数据，但应用程序代码或网页中的脚本编写语言通常会访问生产 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 服务，这些服务也可用来创建、更新和删除数据。 本主题概述了如何访问[!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]客户端应用程序中的源。  
  
## <a name="accessing-and-changing-data-using-rest-semantics"></a>使用 REST 语义访问和更改数据  
 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 有助于保证公开的服务之间的互操作性[!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]馈送和使用的应用程序[!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]馈送。 应用程序访问和更改数据在[!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]-基于通过发送特定 HTTP 操作的寻址应该对其执行操作的实体资源的 URI，且请求消息的服务。 如果必须提供实体数据，则会在消息正文中以明确编码的负载的形式提供该数据。  
  
### <a name="http-actions"></a>HTTP 操作  
 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 支持下列 HTTP 操作，以对寻址的资源所表示的实体数据执行创建、读取、更新和删除操作：  
  
-   **HTTP GET** -这是默认操作时从浏览器访问的资源。 请求消息中不提供负载，将返回具有包含所请求数据的负载的响应方法。  
  
-   **HTTP POST** -将新实体数据插入到提供的资源。 将在请求消息的负载中提供要插入的数据。 响应消息的负载包含新建实体的数据。 这包括所有自动生成的键值。 标头还包含用于对新实体资源进行寻址的 URI。  
  
-   **HTTP DELETE** -删除指定的资源表示的实体数据。 请求消息或响应消息中没有负载。  
  
-   **HTTP PUT** -替换现有实体数据请求的资源在使用新的请求消息负载中提供的数据。  
  
-   **HTTP MERGE** -由于执行删除后再仅仅为更改实体数据的数据源中插入的效率低下[!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]引入了新的 HTTP MERGE 操作。 请求消息的负载包含必须在寻址的实体资源中更改的属性。 由于 HTTP 规范中未定义 HTTP MERGE，因此可能需要进行附加处理以便路由 HTTP MERGE 请求，使其通过无法识别 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 的服务器。  
  
 有关详细信息，请参阅[OData:操作](https://go.microsoft.com/fwlink/?LinkId=185792)。  
  
### <a name="payload-formats"></a>负载格式  
 对于 HTTP PUT、HTTP POST 或 HTTP MERGE 请求，请求消息的负载包含向数据服务发送的实体数据。 负载的内容取决于消息的数据格式。 除 DELETE 外，所有操作的 HTTP 响应也都包含这样一个负载。 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 访问和更改数据与服务支持使用以下负载格式：  
  
-   **Atom** -由基于 XML 的消息编码，可为定义[!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]作为 Atom 发布协议 (AtomPub) 通过 HTTP 启用数据交换，为 Web 源、 播客、 wikis 和基于 XML 的 Internet 功能的扩展。 有关详细信息，请参阅[OData:Atom 格式](https://go.microsoft.com/fwlink/?LinkId=185794)。  
  
-   **JSON** -JavaScript 对象表示法 (JSON) 是一种轻型数据交换格式，基于 JavaScript 编程语言的子集。 有关详细信息，请参阅[OData:JSON 格式](https://go.microsoft.com/fwlink/?LinkId=185795)。  
  
 将在 HTTP 请求消息的标头中请求负载的消息格式。 有关详细信息，请参阅[OData:操作](https://go.microsoft.com/fwlink/?LinkID=185792)。  
  
## <a name="accessing-and-changing-data-using-client-libraries"></a>使用客户端库访问和更改数据  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 包括一些客户端库，使您能够更轻松地使用[!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]源从.NET Framework 和基于 Silverlight 的客户端应用程序。 这些库简化了 HTTP 消息的发送和接收。 它们还可将消息负载转换为代表实体数据的 CLR 对象。 客户端库具有两个核心类 <xref:System.Data.Services.Client.DataServiceContext> 和 <xref:System.Data.Services.Client.DataServiceQuery%601>。 通过使用这些类，可以查询数据服务，然后作为 CLR 对象使用返回的实体数据。 有关详细信息，请参阅[WCF Data Services 客户端库](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)并[WCF 数据服务 (Silverlight)](https://docs.microsoft.com/previous-versions/windows/silverlight/dotnet-windows-silverlight/cc838234(v=vs.95))。  
  
 可以使用**添加服务引用**对话框在 Visual Studio 中添加对数据服务的引用。 此工具将向所引用的数据服务请求服务元数据，然后生成代表数据服务的 <xref:System.Data.Services.Client.DataServiceContext>，并生成代表实体的客户端数据服务类。 有关详细信息，请参阅[生成数据服务客户端库](../../../../docs/framework/data/wcf/generating-the-data-service-client-library-wcf-data-services.md)。  
  
 有现成的编程库可用于使用[!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]源中其他类型的客户端应用程序。 有关详细信息，请参阅[OData SDK](https://go.microsoft.com/fwlink/?LinkId=185796)。  
  
## <a name="see-also"></a>请参阅
- [访问数据服务资源](../../../../docs/framework/data/wcf/accessing-data-service-resources-wcf-data-services.md)
- [快速入门](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)
