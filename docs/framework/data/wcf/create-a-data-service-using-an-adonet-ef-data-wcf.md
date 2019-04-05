---
title: 如何：创建数据服务使用 ADO.NET 实体框架数据源 （WCF 数据服务）
ms.date: 08/24/2018
helpviewer_keywords:
- WCF Data Services, providers
- WCF Data Services, Entity Framework
ms.assetid: 6d11fec8-0108-42f5-8719-2a7866d04428
ms.openlocfilehash: b2adf4fe0d510f65db5bded715f084a4d7e016b6
ms.sourcegitcommit: d2ccb199ae6bc5787b4762e9ea6d3f6fe88677af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56093094"
---
# <a name="how-to-create-a-data-service-using-an-adonet-entity-framework-data-source-wcf-data-services"></a>如何：创建数据服务使用 ADO.NET 实体框架数据源 （WCF 数据服务）

WCF 数据服务公开实体数据作为数据服务。 如果数据源为关系数据库，则此实体数据是由 [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)][!INCLUDE[adonet_ef](../../../../includes/adonet-ef-md.md)]提供的。 本主题演示如何创建[!INCLUDE[adonet_ef](../../../../includes/adonet-ef-md.md)]-基于 Visual Studio Web 应用程序，基于现有数据库和使用此数据模型来创建新的数据服务中的数据模型。

[!INCLUDE[adonet_ef](../../../../includes/adonet-ef-md.md)]还提供了可以生成一个命令行工具[!INCLUDE[adonet_ef](../../../../includes/adonet-ef-md.md)]模型之外的 Visual Studio 项目。 有关详细信息，请参阅[如何：使用 EdmGen.exe 生成模型和映射文件](../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md)。

## <a name="to-add-an-entity-framework-model-that-is-based-on-an-existing-database-to-an-existing-web-application"></a>将基于现有数据库的实体框架模型添加到现有 Web 应用程序

1. 上**项目**菜单上，单击**添加** > **新项**。

2. 在中**模板**窗格中，单击**数据**类别中，并选择**ADO.NET 实体数据模型**。

3. 输入模型名称，然后单击**添加**。

     将显示“[!INCLUDE[adonet_edm](../../../../includes/adonet-edm-md.md)]向导”的第一页。

4. 在中**选择模型内容**对话框中，选择**从数据库生成**。 然后，单击 **“下一步”**。

5. 单击**新的连接**按钮。

6. 在中**连接属性**对话框中，键入你的服务器名称、 选择身份验证方法中，键入数据库名称，然后单击**确定**。

     **选择数据连接**对话框以数据库的连接设置更新。

7. 絋粄**将实体连接设置保存为 App.Config 中：** 选中复选框。 然后，单击 **“下一步”**。

8. 在中**选择数据库对象**对话框中，选择的所有数据库对象计划要在数据服务中公开。

    > [!NOTE]
    > 数据服务不自动公开数据模型中包含的对象。 它们必须由服务本身显式公开。 有关详细信息，请参阅[数据服务配置](../../../../docs/framework/data/wcf/configuring-the-data-service-wcf-data-services.md)。

9. 单击**完成**以完成向导。

     这将基于特定数据库创建默认数据模型。 
  [!INCLUDE[adonet_ef](../../../../includes/adonet-ef-md.md)]允许对数据模型进行自定义。 有关详细信息，请参阅[实体数据模型工具任务](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738480(v=vs.100))。

## <a name="to-create-the-data-service-by-using-the-new-data-model"></a>使用新数据模型创建数据服务

1. 在 Visual Studio 中，打开代表数据模型的 .edmx 文件。

2. 在中**模型浏览器**，右键单击该模型，单击**属性**，然后记下实体容器的名称。

3. 在中**解决方案资源管理器**，右键单击名称你[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]项目，然后依次**添加** > **新项**。

4. 在中**添加新项**对话框中，选择**WCF 数据服务**中的模板**Web**类别。

   ![在 Visual Studio 2015 中的 WCF 数据服务项模板](media/wcf-data-service-item-template.png)

   > [!NOTE]
   > **WCF 数据服务**模板现已推出 Visual Studio 2015，但未在 Visual Studio 2017。

5. 提供服务的名称，然后单击**确定**。

     Visual Studio 将为新服务创建 XML 标记和代码文件。 默认情况下，代码编辑器窗口将打开。

6. 在数据服务代码中，将用于定义数据服务的类定义中的注释 `/* TODO: put your data source class name here */` 替换为从 <xref:System.Data.Objects.ObjectContext> 类继承且作为数据模型的实体容器的类型，如步骤 2 中所述。

7. 在数据服务代码中，启用经过授权的客户端来访问数据服务公开的实体集。 有关详细信息，请参阅[创建数据服务](../../../../docs/framework/data/wcf/creating-the-data-service.md)。

8. 若要使用 Web 浏览器测试 Northwind.svc 数据服务，请按照本主题中的说明[从 Web 浏览器访问服务](../../../../docs/framework/data/wcf/accessing-the-service-from-a-web-browser-wcf-data-services-quickstart.md)。

## <a name="see-also"></a>请参阅

- [定义 WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)
- [数据服务提供程序](../../../../docs/framework/data/wcf/data-services-providers-wcf-data-services.md)
- [如何：创建数据服务使用反射提供程序](../../../../docs/framework/data/wcf/create-a-data-service-using-rp-wcf-data-services.md)
- [如何：创建使用 LINQ to SQL 数据源的数据服务](../../../../docs/framework/data/wcf/create-a-data-service-using-linq-to-sql-wcf.md)