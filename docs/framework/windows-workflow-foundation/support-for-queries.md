---
title: 查询支持
ms.date: 03/30/2017
ms.assetid: 093c22f5-3294-4642-857a-5252233d6796
ms.openlocfilehash: 2314a111cb4c4b82cacd91b7638ef0c8eaba5c3c
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57711992"
---
# <a name="support-for-queries"></a>查询支持
SQL 工作流实例存储中记录了存储区中的一组已知属性。 用户可以根据这些属性查询实例。 下面的列表包含这些已知属性的一部分：  
  
-   **站点名称。** 包含服务的网站的名称。  
  
-   **相对应用程序路径。** 应用程序相对于网站的路径。  
  
-   **相对服务路径。** 服务相对于应用程序的路径。  
  
-   **服务名称。** 服务的名称。  
  
-   **服务 Namespace。** 服务使用的命名空间的名称。  
  
-   **当前计算机。**  
  
-   **上一计算机**。 上次运行工作流服务实例的计算机。  
  
> [!NOTE]
>  对于使用工作流服务主机的自承载方案，仅填充最后四个属性。 对于工作流应用程序方案，仅填充最后一个属性。  
  
 工作流运行时为前三个属性提供值。 工作流服务主机提供的值**挂起原因**属性。 SQL 工作流实例存储自身提供值的**上次更新的计算机**属性。  
  
 使用 SQL 工作流实例存储的功能还可以指定自定义属性，您可以在持久性数据库中存储这些属性的值并且在查询中使用这些属性。 有关自定义促销的详细信息，请参阅[存储扩展性](store-extensibility.md)。  
  
## <a name="views"></a>Views  
 实例存储区包含下列视图。 请参阅[暂留数据库架构](persistence-database-schema.md)的更多详细信息。  
  
### <a name="the-instances-view"></a>Instances 视图  
 Instances 视图包含下列字段：  
  
1.  **Id**  
  
2.  **PendingTimer**  
  
3.  **CreationTime**  
  
4.  **LastUpdatedTime**  
  
5.  **ServiceDeploymentId**  
  
6.  **SuspensionExceptionName**  
  
7.  **SuspensionReason**  
  
8.  **ActiveBookmarks**  
  
9. **CurrentMachine**  
  
10. **LastMachine**  
  
11. **ExecutionStatus**  
  
12. **IsInitialized**  
  
13. **IsSuspended**  
  
14. **IsCompleted**  
  
15. **EncodingOption**  
  
16. **ReadWritePrimitiveDataProperties**  
  
17. **WriteOnlyPrimitiveDataProperties**  
  
18. **ReadWriteComplexDataProperties**  
  
19. **WriteOnlyComplexDataProperties**  
  
### <a name="the-servicedeployments-view"></a>ServiceDeployments 视图  
 ServiceDeployments 视图包含下列字段：  
  
1.  **SiteName**  
  
2.  **RelativeServicePath**  
  
3.  **RelativeApplicationPath**  
  
4.  **ServiceName**  
  
5.  **ServiceNamespace**  
  
### <a name="the-instancepromotedproperties-view"></a>InstancePromotedProperties 视图  
 InstancePromotedProperties 视图包含下列字段。 有关升级的属性的详细信息，请参阅[存储扩展性](store-extensibility.md)主题。  
  
1.  **InstanceId**  
  
2.  **EncodingOption**  
  
3.  **PromotionName**  
  
4.  **Value #** (一系列中的字段**Value1**到**Value64**)。
