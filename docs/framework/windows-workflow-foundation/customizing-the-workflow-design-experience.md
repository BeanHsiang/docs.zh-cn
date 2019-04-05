---
title: 自定义工作流设计体验
ms.date: 03/30/2017
helpviewer_keywords:
- extending [WF], Workflow Designer
ms.assetid: 98135077-0f5d-4d16-9337-01094e843537
ms.openlocfilehash: 2d6ef24d00baa4df6dfc8e0af69c1d489b79a41f
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57724645"
---
# <a name="customizing-the-workflow-design-experience"></a>自定义工作流设计体验

在 [!INCLUDE[wfd1](../../../includes/wfd1-md.md)] 中，已经对用于设计自定义活动以及重新承载 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] 的方案进行了大量简化。 现在，开发和部署工作变得更轻松、更灵活。 主要的基础更改是新的活动设计器编程模型构建在 Windows Presentation Foundation (WPF)。 这使您能够以声明方式定义活动设计器，并且可以相当轻松地在其他应用程序中重新承载 [!INCLUDE[wfd2](../../../includes/wfd2-md.md)]。 在重新承载时，可以开发自定义表达式编辑器来支持 IntelliSense 或简化的表达式域。 使用 Windows Communication Foundation (WCF) 的集成已变得更加无缝使用工作流服务使用。 可使用自定义活动设计器和模型项树来增强重新承载的工作流设计器中的设计时体验。

## <a name="in-this-section"></a>本节内容

 [使用自定义活动设计器和模板](using-custom-activity-designers-and-templates.md)

 介绍如何创建新的自定义活动设计器和模板。

 [重新托管工作流设计器](rehosting-the-workflow-designer.md)

 介绍如何重新托管[!INCLUDE[wfd1](../../../includes/wfd1-md.md)]之外 Visual Studio 以及如何显示验证错误。

 [使用自定义表达式编辑器](using-a-custom-expression-editor.md)

 介绍如何实现一个自定义表达式编辑器来使用 Visual Studio 2010 之外重新承载的工作流设计器。

## <a name="reference"></a>参考

<xref:System.Activities.Presentation.ActivityDesigner>

## <a name="see-also"></a>请参阅

- [扩展 Windows Workflow Foundation](extend.md)
- [设计器](./samples/designer.md)
- [自定义活动设计器](./samples/custom-activity-designers.md)
- [重新承载设计器](./samples/designer-rehosting.md)