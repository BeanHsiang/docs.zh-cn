---
title: 大写约定
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- camel-case names [.NET Framework]
- class library design guidelines [.NET Framework], capitalization
- Pascal-case names [.NET Framework]
- case sensitivity, capitalization conventions
- names [.NET Framework], capitalization
ms.assetid: 4c4ea526-9203-486f-b72d-29d61c5b3c6d
author: KrzysztofCwalina
ms.openlocfilehash: 9a4cf94ca7fcada7dfc0886422b373abc807a0fe
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54670168"
---
# <a name="capitalization-conventions"></a>大写约定
本章中的准则列出了一种针对用例的简单方法，当统一应用此方法时，可以使类型、成员和参数的标识符易于阅读。  
  
## <a name="capitalization-rules-for-identifiers"></a>标识符的大小写规则  
 若要区分标识符中的单词，请将标识符中每个单词的首字母大写。 不要使用下划线来区分单词，也不要为此在标识符中的任何位置使用下划线。 根据标识符的使用情况，可以通过两种适当的方法将标识符大写：  
  
-   PascalCasing  
  
-   camelCasing  
  
 PascalCasing 约定用于除参数名称之外的所有标识符，将每个单词的第一个字符大写（包括超过两个字母的首字母缩写），如以下示例所示：  
  
 `PropertyDescriptor`  
 `HtmlTag`  
  
 这里有一种特殊情况，即遇到两个字母的首字母缩略词时，两个字母都要大写，如下面的标识符所示：  
  
 `IOStream`  
  
 camelCasing 约定仅用于参数名称，将除第一个单词之外的每个单词的第一个字符大写，如以下示例所示。 该示例还显示，以 camelCasing 标识符开始的双字母缩写词都是小写的。  
  
 `propertyDescriptor`  
 `ioStream`  
 `htmlTag`  
  
 **✓ 请** 将 PascalCasing 用于包含多个单词的所有公共成员、类型和命名空间名称。  
  
 **✓ 请** 将 camelCasing 用于参数名称。  
  
 下表介绍了不同类型的标识符的大小写规则。  
  
|标识符|大小写|示例|  
|----------------|------------|-------------|  
|命名空间|帕斯卡命名法|`namespace System.Security { ... }`|  
|类型|帕斯卡命名法|`public class StreamReader { ... }`|  
|接口|帕斯卡命名法|`public interface IEnumerable { ... }`|  
|方法|帕斯卡命名法|`public class Object {` <br />  `public virtual string ToString();` <br /> `}`|  
|属性|帕斯卡命名法|`public class String {` <br />  `public int Length { get; }` <br /> `}`|  
|事件|帕斯卡命名法|`public class Process {` <br />  `public event EventHandler Exited;` <br /> `}`|  
|字段|帕斯卡命名法|`public class MessageQueue {` <br />  `public static readonly TimeSpan` <br /> `InfiniteTimeout;` <br /> `}` <br /> `public struct UInt32 {` <br />  `public const Min = 0;` <br /> `}`|  
|枚举值|帕斯卡命名法|`public enum FileMode {` <br />  `Append,` <br />  `...` <br /> `}`|  
|参数|Camel|`public class Convert {` <br />  `public static int ToInt32(string value);` <br /> `}`|  
  
## <a name="capitalizing-compound-words-and-common-terms"></a>复合词和常用术语的大写  
 出于大写的目的，大多数复合词被视为单个词。  
  
 **X DO NOT要** 将所谓封闭形式的复合词中的每个单词大写。  
  
 下面是以单个单词形式拼写的复合词，例如 endpoint。 根据大小写准则，请将封闭形式的复合词视为单个单词。 请使用最新字典确定复合词是否以封闭形式拼写。  
  
|帕斯卡命名法|Camel|Not|  
|------------|-----------|---------|  
|`BitFlag`|`bitFlag`|`Bitflag`|  
|`Callback`|`callback`|`CallBack`|  
|`Canceled`|`canceled`|`Cancelled`|  
|`DoNot`|`doNot`|`Don't`|  
|`Email`|`email`|`EMail`|  
|`Endpoint`|`endpoint`|`EndPoint`|  
|`FileName`|`fileName`|`Filename`|  
|`Gridline`|`gridline`|`GridLine`|  
|`Hashtable`|`hashtable`|`HashTable`|  
|`Id`|`id`|`ID`|  
|`Indexes`|`indexes`|`Indices`|  
|`LogOff`|`logOff`|`LogOut`|  
|`LogOn`|`logOn`|`LogIn`|  
|`Metadata`|`metadata`|`MetaData, metaData`|  
|`Multipanel`|`multipanel`|`MultiPanel`|  
|`Multiview`|`multiview`|`MultiView`|  
|`Namespace`|`namespace`|`NameSpace`|  
|`Ok`|`ok`|`OK`|  
|`Pi`|`pi`|`PI`|  
|`Placeholder`|`placeholder`|`PlaceHolder`|  
|`SignIn`|`signIn`|`SignOn`|  
|`SignOut`|`signOut`|`SignOff`|  
|`UserName`|`userName`|`Username`|  
|`WhiteSpace`|`whiteSpace`|`Whitespace`|  
|`Writable`|`writable`|`Writeable`|  
  
## <a name="case-sensitivity"></a>区分大小写  
 可以在 CLR 上运行的语言不要求区分大小写，尽管有些语言要求。 即使你的语言支持该功能，其他可能访问你的框架的语言也可能不支持。 因此，任何可从外部访问的 API 都不能仅依赖于大小写来区分同一上下文中的两个名称。  
  
 **X DO NOT要** 假定所有编程语言都区分大小写。 它们不是这样的。 名称不能仅通过大小写来区分。  
  
 *部分版权 © 2005, 2009 Microsoft Corporation。保留所有权利。*  
  
 *经 Pearson Education, Inc 授权，转载自[框架设计准则：可重用的 .NET 库的约定、习惯用语和模式，第 2 版](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 作者：Krzysztof Cwalina 和 Brad Abrams，由 Addison Wesley Professional 于 2008 年 10 月 22 日印发，作为 Microsoft Windows 开发系列的一部分。*  
  
## <a name="see-also"></a>请参阅

- [框架设计指南](../../../docs/standard/design-guidelines/index.md)
- [命名规则](../../../docs/standard/design-guidelines/naming-guidelines.md)
