---
title: Operation 类
ms.date: 03/30/2017
ms.assetid: b19d1496-ef06-4d0c-b2ae-e728ec00cca0
ms.openlocfilehash: 9453d67854bb8439891661b07e3ab3aa373e23eb
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54668296"
---
# <a name="operation-class"></a>Operation 类
操作  
  
## <a name="syntax"></a>语法  
  
```csharp
class Operation  
{  
  string Action;  
  boolean AsyncPattern;  
  Behavior Behaviors[];  
  boolean IsCallback;  
  boolean IsInitiating;  
  boolean IsOneWay;  
  boolean IsTerminating;  
  string MethodSignature;  
  string Name;  
  string ParameterTypes[];  
  string ReplyAction;  
  string ReturnType;  
};  
```  
  
## <a name="methods"></a>方法  
 Operation 类不定义任何方法。  
  
## <a name="properties"></a>Properties  
 Operation 类具有下列属性：  
  
### <a name="action"></a>操作  
 数据类型：String  
  
 访问类型：只读  
  
 请求消息的 WS-Addressing 操作。  
  
### <a name="asyncpattern"></a>AsyncPattern  
 数据类型：Boolean  
  
 访问类型：只读  
  
 指示操作以异步方式使用实现`Begin`[左/右尖括号] 和`End`[左/右尖括号] 方法对服务协定中的。  
  
### <a name="behaviors"></a>Behaviors  
 数据类型：行为数组  
  
 访问类型：只读  
  
 与此操作关联的行为。  
  
### <a name="iscallback"></a>IsCallback  
 数据类型：Boolean  
  
 访问类型：只读  
  
 如果操作为回调操作，则为 True。  
  
### <a name="isinitiating"></a>IsInitiating  
 数据类型：Boolean  
  
 访问类型：只读  
  
 指示方法是否实现了可以启动服务器上的某个会话的操作。  
  
### <a name="isoneway"></a>IsOneWay  
 数据类型：Boolean  
  
 访问类型：只读  
  
 指示操作是否返回答复消息。  
  
### <a name="isterminating"></a>IsTerminating  
 数据类型：Boolean  
  
 访问类型：只读  
  
 指示操作是否返回答复消息。  
  
### <a name="methodsignature"></a>MethodSignature  
 数据类型：String  
  
 访问类型：只读  
  
 操作的方法签名。  
  
### <a name="name"></a>name  
 数据类型：String  
  
 访问类型：只读  
  
 操作的名称。  
  
### <a name="parametertypes"></a>ParameterTypes  
 数据类型：String array  
  
 访问类型：只读  
  
 操作的参数类型。  
  
### <a name="replyaction"></a>ReplyAction  
 数据类型：String  
  
 访问类型：只读  
  
 用于该操作答复消息的 SOAP 操作的值。  
  
### <a name="returntype"></a>ReturnType  
 数据类型：String  
  
 访问类型：只读  
  
 操作的返回类型。  
  
## <a name="requirements"></a>要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|-----------------------------------|  
|命名空间|已在 root\ServiceModel 中定义|  
  
## <a name="see-also"></a>请参阅
- <xref:System.ServiceModel.Description.OperationDescription>
