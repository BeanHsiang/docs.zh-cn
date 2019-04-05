---
title: 使用 Activity 类的工作流活动创作
ms.date: 03/30/2017
ms.assetid: 7b7b1c66-f093-43c3-b4d1-7173b46516da
ms.openlocfilehash: abdabc46aa54e19d5a04c5b34d6d2b9be07488d6
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57711858"
---
# <a name="workflow-activity-authoring-using-the-activity-class"></a>使用 Activity 类的工作流活动创作
若要创建使用 Windows Workflow Foundation (WF) 中的活动的最基本方法[!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)]是创建继承的类<xref:System.Activities.Activity>，创建功能通过组装自定义活动或活动从[内置活动库](net-framework-4-5-built-in-activity-library.md)。 本主题演示如何创建向控制台写入两个消息的活动。

### <a name="to-create-a-custom-activity-using-the-activity-designer"></a>使用活动设计器创建自定义活动

1.  打开 Visual Studio 2012。

2.  依次选择“文件”、“新建”和“项目”。 选择**Workflow 4.0**下**Visual C#** 中**项目类型**窗口中，然后选择**v2010**节点。 选择**活动库**中**模板**窗口。 将新项目命名为 HelloActivity。

3.  打开新的活动。  将 <xref:System.Activities.Statements.Sequence> 活动从工具箱拖到设计器图面。

4.  将 <xref:System.Activities.Statements.WriteLine> 活动拖到 <xref:System.Activities.Statements.Sequence> 活动中。 输入`"Hello World"`（带引号） 入**文本**字段。

5.  将第二个 <xref:System.Activities.Statements.WriteLine> 活动拖到 <xref:System.Activities.Statements.Sequence> 活动中并将其放置在第一个活动的下面。 输入`"Goodbye"`（带引号） 入**文本**字段。
