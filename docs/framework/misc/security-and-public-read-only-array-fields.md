---
title: 安全和公共只读数组字段
ms.date: 03/30/2017
helpviewer_keywords:
- security [.NET Framework], public read-only array fields
ms.assetid: 3df28dee-2a9f-40ff-9852-bfdbe59c27f3
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 03f3ce51eaab9e08d5f05932d9360adc4fd2110f
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54560980"
---
# <a name="security-and-public-read-only-array-fields"></a>安全和公共只读数组字段
切勿使用托管库的只读公共数组字段来定义边界行为或应用程序的安全性，因为可以修改公共的只读数组字段。  
  
## <a name="remarks"></a>备注  
 某些.NET framework 类包括只读、 只包含特定于平台的边界参数的公共字段。  例如，<xref:System.IO.Path.InvalidPathChars>字段是一个数组，其中描述的文件路径字符串中不允许使用的字符。  许多类似字段是存在于整个.NET Framework。  
  
 公共只读字段的值如<xref:System.IO.Path.InvalidPathChars>可以通过代码或共享您的代码的应用程序域的代码修改。  不应使用如下的只读公共数组字段来定义您的应用程序边界行为。  如果这样做，恶意代码可以更改边界定义，并以意外的方式使用你的代码。  
  
 在版本 2.0 及更高版本的.NET Framework 中，应使用返回一个新数组，而不是使用公共数组字段的方法。  例如，而不是使用<xref:System.IO.Path.InvalidPathChars>字段中，应使用<xref:System.IO.Path.GetInvalidPathChars%2A>方法。  
  
 请注意，.NET Framework 类型不使用公共字段在内部定义边界类型。  相反，.NET Framework 使用单独的私有字段。  更改这些公共字段的值不会更改.NET Framework 类型的行为。  
  
## <a name="see-also"></a>请参阅
- [安全编码准则](../../../docs/standard/security/secure-coding-guidelines.md)
