---
title: 配置工作流服务中的序列化
ms.date: 03/30/2017
ms.assetid: aa70b290-a2ee-4c3c-90ea-d0a7665096ae
ms.openlocfilehash: 0e0f03a30aa8e8679cf849aa75948e0bc2314fe5
ms.sourcegitcommit: 69bf8b719d4c289eec7b45336d0b933dd7927841
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/14/2019
ms.locfileid: "57843924"
---
# <a name="configuring-serialization-in-a-workflow-service"></a>配置工作流服务中的序列化
工作流服务是 Windows Communication Foundation (WCF) 服务，因此可以选择是否使用任一<xref:System.Runtime.Serialization.DataContractSerializer>（默认值） 或<xref:System.Xml.Serialization.XmlSerializer>。 编写非工作流服务时，将在服务或操作协定上指定要使用的序列化程序的类型。 创建 WCF 工作流服务时未指定这些协定在代码中，但而不是它们在生成运行时通过协定推理。 有关协定推理的详细信息，请参阅[在工作流中使用协定](../../../../docs/framework/wcf/feature-details/using-contracts-in-workflow.md)。  序列化程序是使用 <xref:System.ServiceModel.Activities.Receive.SerializerOption%2A> 属性指定的。 这可在设计器中进行设置，如下图所示。  
  
 ![在属性窗口中设置 SerializerOption 属性。](./media/configuring-serialization-in-a-workflow-service/setting-serializer-property.png)  
  
 序列化程序也可在代码中进行设置，如下面的示例所示。  
  
```csharp  
Receive approveExpense = new Receive  
            {  
                OperationName = "ApproveExpense",  
                CanCreateInstance = true,  
                ServiceContractName = "FinanceService",  
                SerializerOption = SerializerOption.DataContractSerializer,  
                Content = ReceiveContent.Create(new OutArgument<Expense>(expense))  
            };  
```  
  
  也可在工作流服务上指定已知类型。 有关已知类型的详细信息，请参阅[Data Contract Known Types](data-contract-known-types.md)。 可在设计器或代码中指定已知类型。 若要在设计器中指定已知的类型，请单击中的 KnownTypes 属性旁边的省略号按钮**属性窗口**为<xref:System.ServiceModel.Activities.Receive>活动，如以下插图所示。   
  
 ![KnownTypes 属性对话框的屏幕截图。](./media/configuring-serialization-in-a-workflow-service/known-types-properties.png)  
  
 这将显示类型集合编辑器，可用于搜索和指定已知的类型。  
  
 ![类型集合编辑器的屏幕截图。](./media/configuring-serialization-in-a-workflow-service/type-collection-editor.gif)  
  
 单击**添加新类型**链接并使用下拉菜单选择或搜索某个类型将添加到已知的类型集合。 若要在代码中指定已知类型，请使用 <xref:System.ServiceModel.Activities.Receive.KnownTypes%2A> 属性，如下面的示例所示。  
  
```csharp
Receive approveExpense = new Receive  
            {  
                OperationName = "ApproveExpense",  
                CanCreateInstance = true,  
                ServiceContractName = "FinanceService",  
                SerializerOption = SerializerOption.DataContractSerializer,  
                Content = ReceiveContent.Create(new OutArgument<Expense>(expense))  
            };  
            approveExpense.KnownTypes.Add(typeof(Travel));  
            approveExpense.KnownTypes.Add(typeof(Meal));  
```
