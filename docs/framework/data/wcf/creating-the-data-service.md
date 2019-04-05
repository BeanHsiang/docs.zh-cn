---
title: 在 Visual Studio 中创建 WCF 数据服务
ms.date: 08/24/2018
dev_langs:
- csharp
- vb
ms.assetid: 34d1d971-5e18-4c22-9bf6-d3612e27ea59
ms.openlocfilehash: 361582866dabf51665e1dc94fdc49e8710d8ad3e
ms.sourcegitcommit: d2ccb199ae6bc5787b4762e9ea6d3f6fe88677af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56091820"
---
# <a name="create-the-data-service"></a>创建数据服务

在本主题中，创建使用 WCF 数据服务公开的示例数据服务[!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)]基于 Northwind 示例数据库的源。 此任务涉及以下几个基本步骤：

1. 创建 ASP.NET Web 应用程序。

2. 使用实体数据模型工具定义数据模型。

3. 向 Web 应用程序添加数据服务。

4. 启用对数据服务的访问。

## <a name="create-the-aspnet-web-app"></a>创建 ASP.NET web 应用

1. 在 Visual Studio 中，在**文件**菜单中，选择**新建** > **项目**。

1. 在**新的项目**对话框中的，在下，选择 Visual Basic 或 Visual C# **Web**类别中，并选择**ASP.NET Web 应用程序**。

1. 输入`NorthwindService`作为名称的项目，然后选择**确定**。

1. 在中**新的 ASP.NET Web 应用程序**对话框中，选择**空**，然后选择**确定**。

1. （可选）为 Web 应用程序指定一个特定的端口号。 注意： 端口号`12345`这一系列的快速入门主题中使用。

    1. 在中**解决方案资源管理器**，右键单击刚创建的 ASP.NET 项目，然后选择**属性**。

    2. 选择**Web**选项卡，并设置的值**特定端口**向文本框`12345`。

## <a name="define-the-data-model"></a>定义数据模型

1. 在中**解决方案资源管理器**，右键单击 ASP.NET 项目的名称，然后单击**添加** > **新项**。

2. 在中**添加新项**对话框中，选择**数据**类别中，并选择**ADO.NET 实体数据模型**。

3. 对于数据模型的名称，输入`Northwind.edmx`。

4. 在中**实体数据模型向导**，选择**EF 设计器从数据库**，然后单击**下一步**。

5. 连接到数据库的数据模型，通过执行以下步骤之一，然后单击**下一步**:

    -   如果没有已配置的数据库连接，请单击**新的连接**和创建新的连接。 有关详细信息，请参阅[如何：创建连接到 SQL Server 数据库](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/s4yys16a(v=vs.90))。 此 SQL Server 实例必须附加了 Northwind 示例数据库。

         \- 或 -

    -   如果已配置一个连接到 Northwind 数据库的数据库连接，请从连接列表中选择该连接。

6. 在向导的最后一页中，选中数据库中所有表对应的复选框，并清除视图和存储过程对应的复选框。

7. 单击**完成**以关闭向导。

## <a name="create-the-wcf-data-service"></a>创建 WCF 数据服务

1. 在中**解决方案资源管理器**，右键单击 ASP.NET 项目，然后选择**添加** > **新项**。

2. 在中**添加新项**对话框中，选择**WCF 数据服务**中的项模板**Web**类别。

   ![在 Visual Studio 2015 中的 WCF 数据服务项模板](media/wcf-data-service-item-template.png)

   > [!NOTE]
   > **WCF 数据服务**模板现已推出 Visual Studio 2015，但未在 Visual Studio 2017。

3. 对于服务的名称，键入`Northwind`。

     Visual Studio 将为新服务创建 XML 标记和代码文件。 默认情况下，代码编辑器窗口将打开。 在中**解决方案资源管理器**，该服务具有扩展名的名称 Northwind *。 svc.cs*或 *。 svc.vb*。

4. 在数据服务的代码中，用数据模型的实体容器的类型（在此示例中为 `/* TODO: put your data source class name here */`）替换定义数据服务的类定义中的注释 `NorthwindEntities`。 该类定义应如下所示：

     [!code-csharp[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria quickstart service/cs/northwind.svc.cs#servicedefinition)]
     [!code-vb[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria quickstart service/vb/northwind.svc.vb#servicedefinition)]

## <a name="enable-access-to-data-service-resources"></a>启用对数据服务资源的访问

1. 在数据服务的代码中，用下列代码替换 `InitializeService` 函数中的占位符代码：

     [!code-csharp[Astoria Quickstart Service#AllReadConfig](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria quickstart service/cs/northwind.svc.cs#allreadconfig)]
     [!code-vb[Astoria Quickstart Service#AllReadConfig](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria quickstart service/vb/northwind.svc.vb#allreadconfig)]

     这使得授权客户端能够对指定实体集的资源进行读写访问。

    > [!NOTE]
    > 任何可以访问该 ASP.NET 应用程序的客户端也能够访问由数据服务公开的资源。 在生产数据服务中，为防止对资源进行未经授权的访问，还应保护应用程序本身的安全。 有关更多信息，请参见 [Securing WCF Data Services](../../../../docs/framework/data/wcf/securing-wcf-data-services.md)。

## <a name="next-steps"></a>后续步骤

已成功创建新的数据服务公开 OData 源的基于 Northwind 示例数据库，并已启用对该源的 ASP.NET Web 应用程序上具有权限的客户端的访问权限。 接下来，将从 Visual Studio 启动数据服务并访问 OData 数据源提交 HTTP GET 请求通过 Web 浏览器：

> [!div class="nextstepaction"]
> [从 web 浏览器访问服务](../../../../docs/framework/data/wcf/accessing-the-service-from-a-web-browser-wcf-data-services-quickstart.md)

## <a name="see-also"></a>请参阅

- [ADO.NET 实体数据模型工具](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399249(v=vs.100))