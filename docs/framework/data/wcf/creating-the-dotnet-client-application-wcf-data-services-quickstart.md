---
title: 创建 .NET Framework 客户端应用程序（WCF 数据服务快速入门）
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 41ade767-eeab-437d-9121-9797e8fb8045
ms.openlocfilehash: 2f48f9486c5d29fc0b70e4487a12a1c499235cba
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54732643"
---
# <a name="creating-the-net-framework-client-application-wcf-data-services-quickstart"></a>创建 .NET Framework 客户端应用程序（WCF 数据服务快速入门）

这是 WCF 数据服务快速入门的最后一项任务。 在此任务中，你将添加到解决方案的控制台应用程序，请添加对引用[!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)]馈送到此新的客户端应用程序，并访问 OData 数据源从客户端应用程序通过使用生成的客户端数据服务类和客户端库.

> [!NOTE]
> 访问数据源不需要基于 .NET Framework 的客户端应用程序。 可以通过任何应用程序组件，使用 OData 源访问数据服务。 有关详细信息，请参阅[在客户端应用程序中使用数据服务](../../../../docs/framework/data/wcf/using-a-data-service-in-a-client-application-wcf-data-services.md)。

## <a name="to-create-the-client-application-by-using-visual-studio"></a>使用 Visual Studio 创建客户端应用程序

1.  在中**解决方案资源管理器**，右键单击该解决方案，单击**添加**，然后单击**新项目**。

2.  在左窗格中，选择**已安装**> [**Visual C#** 或**Visual Basic**] > **Windows 桌面**，然后选择**WPF 应用**模板。

3.  输入`NorthwindClient`以及该项目名称，然后单击**确定**。

4.  打开文件 MainWindow.xaml 并用下列代码替换 XAML 代码：

     [!code-xaml[Astoria Quickstart Client#Window1Xaml](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria quickstart client/vb/window1.xaml#window1xaml)]

## <a name="to-add-a-data-service-reference-to-the-project"></a>在项目中添加数据服务引用

1.  在中**解决方案资源管理器**中右击 NorthwindClient 项目，单击**添加** > **服务引用**，然后单击**发现**.

     这将显示在第一个任务中创建的 Northwind 数据服务。

2.  在中**Namespace**文本框中，键入`Northwind`，然后单击**确定**。

     这将在项目中添加一个新的代码文件，其中包含用于作为对象访问数据服务资源并与其交互的数据类。 这些数据类是在命名空间 `NorthwindClient.Northwind` 中创建的。

## <a name="to-access-data-service-data-in-the-wpf-application"></a>在 WPF 应用程序中访问数据服务数据

1.  在中**解决方案资源管理器**下**NorthwindClient**，右键单击项目，然后单击**添加引用**。

2.  在中**添加引用**对话框中，单击 **.NET**选项卡上，选择 System.Data.Services.Client.dll 程序集，，然后单击**确定**。

3. 在中**解决方案资源管理器**下**NorthwindClient**，打开 MainWindow.xaml 文件的代码页，并添加以下`using`语句 (`Imports`在 Visual Basic 中)。

     [!code-csharp[Astoria Quickstart Client#Using](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria quickstart client/cs/window1.xaml.cs#using)]
     [!code-vb[Astoria Quickstart Client#Using](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria quickstart client/vb/window1.xaml.vb#using)]

3.  将用于查询数据服务并将结果绑定到 <xref:System.Data.Services.Client.DataServiceCollection%601> 的下列代码插入到 `MainWindow` 类：

    > [!NOTE]
    > 必须用承载 Northwind 数据服务的实例的服务器和端口替换主机名 `localhost:12345`。

     [!code-csharp[Astoria Quickstart Client#QueryCode](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria quickstart client/cs/window1.xaml.cs#querycode)]
     [!code-vb[Astoria Quickstart Client#QueryCode](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria quickstart client/vb/window1.xaml.vb#querycode)]

4.  将用于保存更改的下列代码插入到 `MainWindow` 类：

     [!code-csharp[Astoria Quickstart Client#SaveChanges](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria quickstart client/cs/window1.xaml.cs#savechanges)]
     [!code-vb[Astoria Quickstart Client#SaveChanges](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria quickstart client/vb/window1.xaml.vb#savechanges)]

## <a name="to-build-and-run-the-northwindclient-application"></a>生成并运行 NorthwindClient 应用程序

1.  在中**解决方案资源管理器**，右键单击 NorthwindClient 项目并选择**设为启动项目**。

2.  按**F5**启动应用程序。

     这将生成解决方案并启动客户端应用程序。 将从服务请求数据并将其显示在控制台中。

3.  编辑中的值**Quantity**列的数据网格，然后单击**保存**。

     将更改保存到数据服务。

    > [!NOTE]
    > 此版本的 NorthwindClient 应用程序不支持添加和删除实体。

## <a name="next-steps"></a>后续步骤

已成功创建访问的示例 Northwind odata 的客户端应用程序。 你已经完成 WCF Data Services 快速入门 ！

有关从馈送的有关访问 OData 的详细信息[!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]应用程序，请参阅[WCF Data Services 客户端库](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)。

## <a name="see-also"></a>请参阅

- [入门](../../../../docs/framework/data/wcf/getting-started-with-wcf-data-services.md)
- [资源](../../../../docs/framework/data/wcf/wcf-data-services-resources.md)
