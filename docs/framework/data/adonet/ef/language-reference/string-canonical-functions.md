---
title: 字符串规范函数
ms.date: 03/30/2017
ms.assetid: 5e2cbebd-5df3-47c7-b0e2-49a17ab22bfb
ms.openlocfilehash: fbad71fe788eb5653bf4ea8e85a96b71e75bad89
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54607103"
---
# <a name="string-canonical-functions"></a>字符串规范函数
[!INCLUDE[esql](../../../../../../includes/esql-md.md)] 包含字符串规范函数。  
  
## <a name="remarks"></a>备注  
 下表列出了字符串 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 规范函数。  
  
|函数|描述|  
|--------------|-----------------|  
|`Concat(string1, string2)`|返回包含追加了 `string2` 的 `string1` 的字符串。<br /><br /> **参数**<br /><br /> `string1`：字符串`string2`追加。<br /><br /> `string2`：追加到字符串`string1`。<br /><br /> **返回值**<br /><br /> `String`。 如果返回值字符串的长度大于允许的最大长度，则发生错误。<br /><br /> **示例**<br /><br /> `-- The following example returns abcxyz.`<br /><br /> `Concat('abc', 'xyz')`|  
|`Contains(string, target)`|如果 `true` 包含在 `target` 中，则返回 `string`。<br /><br /> **参数**<br /><br /> `string`：搜索字符串。<br /><br /> `target`：搜索目标字符串。<br /><br /> **返回值**<br /><br /> 如果 `true` 包含在 `target` 中，则为 `string`；否则为 `false`。<br /><br /> **示例**<br /><br /> `-- The following example returns true.`<br /><br /> `Contains('abc', 'bc')`|  
|`EndsWith(string, target)`|如果 `true` 以 `target` 结尾，则返回 `string`。<br /><br /> **参数**<br /><br /> `string`：搜索字符串。<br /><br /> `target`：搜索的目标字符串的末尾`string`。<br /><br /> **返回值**<br /><br /> 如果 `True` 以 `string` 结尾，则返回 `target`；否则返回 `false`。<br /><br /> **示例**<br /><br /> `-- The following example returns true.`<br /><br /> `EndsWith('abc', 'bc')` **注意：** 如果使用 SQL Server 数据提供程序，此函数将返回`false`如果将字符串存储在固定的长度字符串列和`target`是一个常量。 在这种情况下，将搜索整个字符串，包括任何填充尾随空格。 一种可能的解决办法是将数据裁剪为固定长度字符串，如下面的示例中所示：`EndsWith(TRIM(string), target)`|  
|`IndexOf(target, string)`|返回 `target` 在 `string` 中的位置，如果没找到则返回 0。 返回 1 指示 `string` 的起始位置。 索引号从 1 开始。<br /><br /> **参数**<br /><br /> `target`：搜索的字符串。<br /><br /> `string`：搜索字符串。<br /><br /> **返回值**<br /><br /> 一个 `Int32`。<br /><br /> **示例**<br /><br /> `-- The following example returns 4.`<br /><br /> `IndexOf('xyz', 'abcxyz')`|  
|`Left(string, length)`|返回 `length` 左侧开始的前 `string` 个字符。 如果 `string` 的长度小于 `length`，则返回整个字符串。<br /><br /> **参数**<br /><br /> `string`：`String`。<br /><br /> `length`：`Int16`， `Int32`， `Int64`，或`Byte`。 `length` 不能小于零。<br /><br /> **返回值**<br /><br /> `String`。<br /><br /> **示例**<br /><br /> `-- The following example returns abc.`<br /><br /> `Left('abcxyz', 3)`|  
|`Length(string)`|返回字符串的 (`Int32`) 长度，以字符为单位。<br /><br /> **参数**<br /><br /> `string`：`String`。<br /><br /> **返回值**<br /><br /> 一个 `Int32`。<br /><br /> **示例**<br /><br /> `-- The following example returns 6.`<br /><br /> `Legth('abcxyz')`|  
|`LTrim(string)`|返回`string`而无需前导空白字符。<br /><br /> **参数**<br /><br /> `String`。<br /><br /> **返回值**<br /><br /> `String`。<br /><br /> **示例**<br /><br /> `-- The following example returns abc.`<br /><br /> `LTrim('   abc')`|  
|`Replace(string1, string2, string3)`|返回 `string1`，其中所有 `string2` 都替换为 `string3`。<br /><br /> **参数**<br /><br /> `String`。<br /><br /> **返回值**<br /><br /> `String`。<br /><br /> **示例**<br /><br /> `-- The following example returns abcxyz.`<br /><br /> `Concat('abc', 'xyz')`|  
|`Reverse(string)`|返回反转字符顺序的 `string`。<br /><br /> **参数**<br /><br /> `String`。<br /><br /> **返回值**<br /><br /> `String`。<br /><br /> **示例**<br /><br /> `-- The following example returns dcba.`<br /><br /> `Reverse('abcd')`|  
|`Right(string, length)`|返回上次`length`字符从`string`。 如果 `string` 的长度小于 `length`，则返回整个字符串。<br /><br /> **参数**<br /><br /> `string`：`String`。<br /><br /> `length`：`Int16`， `Int32`， `Int64`，或`Byte`。 `length` 不能小于零。<br /><br /> **返回值**<br /><br /> `String`。<br /><br /> **示例**<br /><br /> `-- The following example returns xyz.`<br /><br /> `Right('abcxyz', 3)`|  
|`RTrim(string)`|返回`string`没有尾随空格。<br /><br /> **参数**<br /><br /> `String`。<br /><br /> **返回值**<br /><br /> `String`。|  
|`Substring(string, start, length)`|返回字符串的从 `start` 位置开始、长度为 `length` 个字符的子字符串。 start 为 1 指示字符串的第一个字符。 索引号从 1 开始。<br /><br /> **参数**<br /><br /> `string`：`String`。<br /><br /> `start`：`Int16`、`Int32`、`Int64` 和 `Byte`。 `start` 不能小于一。<br /><br /> `length`：`Int16`、`Int32`、`Int64` 和 `Byte`。 `length` 不能小于零。<br /><br /> **返回值**<br /><br /> `String`。<br /><br /> **示例**<br /><br /> `-- The following example returns xyz.`<br /><br /> `Substring('abcxyz', 4, 3)`|  
|`StartsWith(string, target)`|如果 `true` 以 `string` 开头，则返回 `target`。<br /><br /> **参数**<br /><br /> `string`：搜索字符串。<br /><br /> `target`：在开始搜索的目标字符串`string`。<br /><br /> **返回值**<br /><br /> 如果 `True` 以 `string` 开头，则返回 `target`；否则返回 `false`。<br /><br /> **示例**<br /><br /> `-- The following example returns true.`<br /><br /> `StartsWith('abc', 'ab')`|  
|`ToLower(string)`|返回全部大写字符都转换为小写字符的 `string`。<br /><br /> **参数**<br /><br /> `String`。<br /><br /> **返回值**<br /><br /> `String`。<br /><br /> **示例**<br /><br /> `-- The following example returns abc.`<br /><br /> `ToLower('ABC')`|  
|`ToUpper(string)`|返回全部小写字符都转换为大写字符的 `string`。<br /><br /> **参数**<br /><br /> `String`。<br /><br /> **返回值**<br /><br /> `String`。<br /><br /> **示例**<br /><br /> `-- The following example returns ABC.`<br /><br /> `ToUpper('abc')`|  
|`Trim(string)`|返回`string`而无需前导和尾随空格。<br /><br /> **参数**<br /><br /> `String`。<br /><br /> **返回值**<br /><br /> `String`。<br /><br /> **示例**<br /><br /> `-- The following example returns abc.`<br /><br /> `Trim('      abc   ')`|  
  
 如果提供 `null` 输入，则这些函数返回 `null`。  
  
 Microsoft SQL 客户端托管提供程序中提供了等效功能。 有关详细信息，请参阅[用于实体框架函数的 SqlClient](../../../../../../docs/framework/data/adonet/ef/sqlclient-for-ef-functions.md)。  
  
## <a name="see-also"></a>请参阅
- [规范函数](../../../../../../docs/framework/data/adonet/ef/language-reference/canonical-functions.md)
