---
title: 如何：执行 .NET 中的基本字符串控制
description: 查看调用许多字符串方法的示例。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- strings [.NET Framework], examples
ms.assetid: 121d1eae-251b-44c0-8818-57da04b8215e
author: rpetrusha
ms.author: ronpet
ms.custom: seodec18
ms.openlocfilehash: 11f8043745c631a642b437339240cbf06fc8df5b
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53130632"
---
# <a name="how-to-perform-basic-string-manipulations-in-net"></a>如何：执行 .NET 中的基本字符串控制
下面的示例使用[基本字符串操作](../../../docs/standard/base-types/basic-string-operations.md)主题中介绍的一些方法，构造模拟现实应用执行字符串控制的类。 `MailToData` 类将个人的姓名和地址存储在单独的属性中，并提供一种将 `City`、`State` 和 `Zip` 字段合并成向用户显示的单个字符串的方式。 此外，该类允许用户以单个字符串的形式输入将城市、州/省和邮政编码信息；应用程序会自动分析此字符串，并将正确的信息输入到相应的属性中。  
  
 为简单起见，此示例使用带命令行接口的控制台应用程序。  
  
## <a name="example"></a>示例  
 [!code-csharp[Conceptual.String.BasicOps#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/basicops.cs#1)]
 [!code-vb[Conceptual.String.BasicOps#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/basicops.vb#1)]  
  
 执行上面的代码时，系统会要求用户输入其姓名和地址。 应用程序将这些信息放入相应的属性并向用户显示这些信息，同时创建一个显示城市、州/省和邮政编码信息的字符串。  
  
## <a name="see-also"></a>请参阅

- [基本字符串操作](../../../docs/standard/base-types/basic-string-operations.md)
