---
title: 获取示例 SQL Server 数据库的 ADO.NET 代码示例
description: 下载 ADO.NET 文档以及 SQL Server 和管理工具中的代码示例中使用的示例 SQL Server 数据库
ms.date: 01/11/2019
ms.assetid: ef9d69a1-9461-43fe-94bb-7c836754bcb5
ms.openlocfilehash: 5580f06f3d28ed6d70f75b619498ac8de7bc3326
ms.sourcegitcommit: 75567a3cb437009db55949c6092f4e77ed1a9da4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/15/2019
ms.locfileid: "54307287"
---
# <a name="get-the-sample-databases-for-adonet-code-samples"></a>获取示例数据库的 ADO.NET 代码示例

示例和演练中的大量[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]文档使用示例 SQL Server 数据库和 SQL Server Express。 可从 Microsoft 下载这些免费的产品。

## <a name="get-the-northwind-sample-database-for-sql-server"></a>获取 SQL Server 的 Northwind 示例数据库

下载脚本`instnwnd.sql`从以下 GitHub 存储库，用于创建和加载 SQL Server 的 Northwind 示例数据库：

[Microsoft SQL Server 的 Northwind 和 pubs 示例数据库](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/northwind-pubs)

可以使用 Northwind 数据库之前，必须运行下载`instnwnd.sql`脚本文件以使用重新创建的 SQL Server 实例上的数据库[SQL Server Management Studio](#get_ssms)或类似的工具。 按照存储库中的自述文件中的说明。

> [!TIP]
> 如果您正在寻找 Microsoft access Northwind 数据库，请参阅[安装用于 Microsoft Access Northwind 示例数据库](#northwind_access)。

## <a name="northwind_access"></a> 获取 Microsoft Access Northwind 示例数据库

Microsoft Access Northwind 示例数据库在 Microsoft 下载中心上不可用。 若要安装在 Access 中的直接从 Northwind，执行以下操作：

1. 打开访问权限。

1. Enter **Northwind**中**搜索联机模板**框，并选择**Enter**。

1. 在结果屏幕上，选择**Northwind**。 使用 Northwind 数据库的说明打开一个新窗口。

1. 在新窗口中，在**文件名**文字框中，Northwind 数据库的副本提供一个文件名。

1. 选择“创建”。 访问下载 Northwind 数据库，并准备该文件。

1. 此过程完成后，使用欢迎屏幕打开数据库。

## <a name="get-the-adventureworks-sample-database-for-sql-server"></a>获取 AdventureWorks 示例数据库的 SQL Server

从以下 GitHub 存储库的 SQL server 下载 AdventureWorks 示例数据库：

[AdventureWorks 示例数据库](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)

下载一个数据库备份后 (\*.bak) 文件，将备份还原到的 SQL Server 实例使用 SQL Server Management Studio (SSMS)。 请参阅[获取 SQL Server Management Studio](#get_ssms)。

## <a name="get_ssms"></a> 获取 SQL Server Management Studio
如果你想要查看或修改已下载的数据库，可以使用 SQL Server Management Studio (SSMS)。 从以下页面下载 SSMS:

[下载 SQL Server Management Studio (SSMS)](/sql/ssms/download-sql-server-management-studio-ssms) 

您还可以查看和管理 Visual Studio 集成的开发环境 (IDE) 中的数据库。 在中[Visual Studio](https://www.visualstudio.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)，连接到从数据库**SQL Server 对象资源管理器**，或创建到数据库中的数据连接**服务器资源管理器**。 打开从这些资源管理器窗格**视图**菜单。

## <a name="get_sql"></a> Get SQL Server Express

SQL Server Express 是免费的入门级版本可以与应用程序重新发布的 SQL Server。 下载 SQL Server Express 的以下页面：
  
[SQL Server Express Edition](https://www.microsoft.com/sql-server/sql-server-editions-express)

如果您使用的[Visual Studio](https://www.visualstudio.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)，在 Visual Studio 的免费的社区版和专业和更高版本包括 SQL Server Express LocalDB。  

## <a name="see-also"></a>请参阅

- [入门](../../../../../../docs/framework/data/adonet/sql/linq/getting-started.md)
