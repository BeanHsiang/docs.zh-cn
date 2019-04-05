---
title: 在工作流解决方案中添加服务引用
ms.date: 03/30/2017
ms.assetid: 83574cf3-9803-49bc-837f-432936dc9c76
ms.openlocfilehash: 8f1fa4604f1a1873c7063ec3c9dccf08bd0aa0ee
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54549036"
---
# <a name="adding-a-service-reference-in-a-workflow-solution"></a>在工作流解决方案中添加服务引用

在工作流应用程序中添加服务引用后，其工作方式与常规 WCF 应用程序略有不同。 当选择**添加 > 服务引用**和指定服务的 URL、 下载元数据和自定义活动生成，可用于调用 WCF 服务或 WCF 工作流服务添加到的引用。 添加服务引用后，重新生成解决方案，以便构建生成的活动。 之后它们将出现在工作流设计器工具箱中。 但是请注意，仅当在工作流解决方案之内添加服务引用时，这才是可行的。 以下 web 广播揭示了如何在其他类型的项目中添加服务引用：[从 Web 项目中的工作流调用的 WCF 服务](https://go.microsoft.com/fwlink/?LinkId=207725)。

添加对包含相同操作名称的服务的两个或多个服务引用会导致出现问题。 生成的活动将仅调用第一个服务操作。 要解决此问题，请重命名服务操作以使其各不相同，或在每个生成的活动中更改终结点配置名称。

## <a name="see-also"></a>请参阅

- [工作流服务](../../../../docs/framework/wcf/feature-details/workflow-services.md)
- [从 Web 项目中的工作流调用的 WCF 服务](https://go.microsoft.com/fwlink/?LinkId=207725)
