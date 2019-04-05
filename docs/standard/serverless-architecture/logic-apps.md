---
title: Azure 逻辑应用-无服务器应用
description: Azure 逻辑应用可以生成自动将应用集成的可缩放工作流和跨云数据服务，并在本地系统。
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: 14670a8459db3b80b8fbe3139c2675321cf9592c
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53147938"
---
# <a name="azure-logic-apps"></a>Azure 逻辑应用

[Azure 逻辑应用](https://docs.microsoft.com/azure/logic-apps)提供无服务器引擎生成自动化工作流以将应用程序和云服务之间的数据集成，并在本地系统。 生成工作流使用可视化设计器。 可以触发基于事件或计时器和利用连接器再到集成应用程序的工作流，并促进企业到企业 (B2B) 通信。 逻辑应用与 Azure Functions 无缝集成。

![Azure 逻辑应用徽标](./media/logic-apps-logo.png)

个以上的只是连接云服务 （例如函数） 为逻辑应用可以使用云资源 （如队列和数据库）。 此外可以安排在本地与在本地网关的工作流。 例如，可以使用逻辑应用中触发对基于云的事件作出响应的本地 SQL 存储过程或在工作流中的条件逻辑。 详细了解如何[连接到使用 Azure 本地数据网关的本地数据源](https://docs.microsoft.com/azure/analysis-services/analysis-services-gateway)。

![逻辑应用体系结构](./media/logic-apps-architecture.png)

Azure Functions 等启动逻辑应用工作流分别具有一个触发器。 有许多触发器，以便从中进行选择。 以下截图显示了一些更受欢迎的外出时的数百个可用。

![逻辑应用触发器](./media/logic-app-triggers.png)

应用程序触发后，可以使用可视化设计器生成步骤、 循环、 条件和操作。 可为你在后续步骤中使用上一步中引入的任何数据。 下面的工作流从 CosmosDB 数据库加载 Url。 它找到的主机具有`t.co`搜索 Twitter 它们。 如果找到相应的推文，它更新文档的相关推文通过调用一个函数。

![逻辑应用工作流](./media/logic-app-workflow.png)

逻辑应用仪表板显示正在运行的工作流和是否每个运行已完成，不论成功与否的历史记录。 可以导航到任何给定运行并检查每个步骤用于故障排除的数据。 逻辑应用还提供了你可以编辑，但非常适用于复杂的企业工作流的现有模板。

若要了解详细信息，请参阅[Azure 逻辑应用](https://docs.microsoft.com/azure/logic-apps)。

>[!div class="step-by-step"]
>[上一页](application-insights.md)
>[下一页](event-grid.md)