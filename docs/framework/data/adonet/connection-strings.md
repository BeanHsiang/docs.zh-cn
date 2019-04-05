---
title: 在 ADO.NET 中的连接字符串
ms.date: 10/10/2018
ms.assetid: 745c5f95-2f02-4674-b378-6d51a7ec2490
ms.openlocfilehash: 1197335f3ba2a09b6e7303d31bc32383d1fd3436
ms.sourcegitcommit: 69bf8b719d4c289eec7b45336d0b933dd7927841
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/14/2019
ms.locfileid: "57844867"
---
# <a name="connection-strings-in-adonet"></a>在 ADO.NET 中的连接字符串

连接字符串包含作为参数从数据提供程序传递到数据源的初始化信息。 数据提供程序接收的连接字符串的值作为<xref:System.Data.Common.DbConnection.ConnectionString?displayProperty=nameWithType>属性。 提供程序来分析连接字符串，并确保语法正确，以及支持的关键字。 然后<xref:System.Data.Common.DbConnection.Open?displayProperty=nameWithType>方法将已分析的连接参数传递到数据源。 数据源执行进一步的验证，并建立的连接。

## <a name="connection-string-syntax"></a>连接字符串语法

连接字符串是以分号分隔的键/值参数对的列表：

    keyword1=value; keyword2=value;

关键字不区分大小写。 但是，值可能区分大小写，具体取决于数据源。 关键字和值可能包含[空白字符](https://en.wikipedia.org/wiki/Whitespace_character#Unicode)。 在关键字中忽略和不带引号的前导和尾随空格的值。

如果值包含分号[Unicode 控制字符](https://en.wikipedia.org/wiki/Unicode_control_characters)，或前导空格或尾随空格，则必须用单引号或双引号括起来。 例如：

    Keyword=" whitespace  ";
    Keyword='special;character';

它包含的值中可能不是封闭字符。 因此，仅在两个双引号，反之亦然，可以用一个值，包含单引号引起来：

    Keyword='double"quotation;mark';
    Keyword="single'quotation;mark";

引号本身，以及等号，不需要转义，因此以下连接字符串有效：

    Keyword=no "escaping" 'required';
    Keyword=a=b=c

由于直到下一步分号或字符串的末尾读取每个值，后者的示例中的值是`a=b=c`，并最终分号是可选的。

所有连接字符串都共享相同的基本语法上面所述。 已识别的关键字集合取决于提供程序，但是，并已发展多年来从早期的 Api 如*ODBC*。 *.NET Framework*的数据提供程序*SQL Server* (`SqlClient`) 支持很多关键字从较旧的 Api，但更具灵活性并接受同义词的许多常见的连接字符串关键字。

键入了错误可能会导致错误。 例如，`Integrated Security=true`有效，但`IntegratedSecurity=true`将导致错误。

手动构造在运行时从未经验证的用户输入的连接字符串容易受到字符串注入式攻击，并会危及数据源的安全性。 若要解决这些问题*ADO.NET* 2.0 引入[的连接字符串生成器](../../../../docs/framework/data/adonet/connection-string-builders.md)每个 *.NET Framework*数据提供程序。 这些连接字符串生成器公开作为强类型化属性的参数，并使其可以发送到数据源之前验证的连接字符串。

## <a name="in-this-section"></a>本节内容

[连接字符串生成器](../../../../docs/framework/data/adonet/connection-string-builders.md)\
演示如何使用 `ConnectionStringBuilder` 类在运行时构造有效的连接字符串。

[连接字符串和配置文件](../../../../docs/framework/data/adonet/connection-strings-and-configuration-files.md)\
演示如何在配置文件中存储和检索连接字符串。

[连接字符串语法](../../../../docs/framework/data/adonet/connection-string-syntax.md)\
描述如何为 `SqlClient`、`OracleClient`、`OleDb` 和 `Odbc` 配置提供程序专用的连接字符串。

[保护连接信息](../../../../docs/framework/data/adonet/protecting-connection-information.md)\
演示保护用于连接到数据源的信息的各项技术。

## <a name="see-also"></a>请参阅

- [连接到数据源](/cpp/data/odbc/connecting-to-a-data-source)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
