---
title: 设置数值结果表的格式 - C# 参考
ms.custom: seodec18
description: 了解 C# 标准数字格式字符串
ms.date: 09/20/2018
helpviewer_keywords:
- formatting [C#]
- numeric formatting [C#]
- String.Format method
ms.assetid: 120ba537-4448-4c62-8676-7a8fdd98f496
ms.openlocfilehash: 12fe89e3aa63e9d3d8c3f102fe5a01a5f2225375
ms.sourcegitcommit: bdd930b5df20a45c29483d905526a2a3e4d17c5b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53239964"
---
# <a name="formatting-numeric-results-table-c-reference"></a>设置数值结果表的格式（C# 参考）

下表显示了设置数值结果格式的受支持格式说明符。 最后一列中的格式化结果对应于“en-US”<xref:System.Globalization.CultureInfo>。

|格式说明符|说明|示例|结果|  
|----------------------|-----------------|--------------|------------|  
|C 或 c|货币|`string s = $"{2.5:C}";`<br /><br /> `string s = $"{-2.5:C}";`|$2.50<br /><br /> ($2.50)|  
|D 或 d|十进制|`string s = $"{25:D5}";`|00025|  
|E 或 e|指数|`string s = $"{250000:E2}";`|2.50E+005|  
|F 或 f|定点|`string s = $"{2.5:F2}";`<br /><br /> `string s = $"{2.5:F0}";`|2.50<br /><br /> 3|  
|G 或 g|常规|`string s = $"{2.5:G}";`|2.5|  
|N 或 n|Numeric|`string s = $"{2500000:N}";`|2,500,000.00|  
|P 或 p|百分比|`string s = $"{0.25:P}";`|25.00%|  
|R 或 r|往返过程|`string s = $"{2.5:R}";`|2.5|  
|X 或 x|十六进制|`string s = $"{250:X}";`<br /><br /> `string s = $"{0xffff:X}";`|FA<br /><br /> FFFF|  

## <a name="remarks"></a>备注

使用格式说明符可以创建格式字符串。 格式字符串的格式如下：`Axx`，其中

- `A` 是格式说明符，控制应用于数值的格式设置类型。
- `xx` 是精度说明符，影响格式化输出中的位数。 精度说明符值的范围为 0 到 99。

十进制（“D”或“d”）和十六进制（“X”或“x”）格式说明符仅支持用于整型类型。 往返（“R”或“r”）格式说明符仅支持用于 <xref:System.Single>、<xref:System.Double> 和 <xref:System.Numerics.BigInteger> 类型。

下列支持标准数字格式字符串：

- 所有数字类型的一些 `ToString` 方法重载。 例如，可以向 <xref:System.Int32.ToString%28System.String%29?displayProperty=nameWithType> 和 <xref:System.Int32.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> 方法提供数字格式字符串。

- 例如，由 <xref:System.String.Format%2A?displayProperty=nameWithType> 方法提供支持的 .NET [复合格式设置功能](../../../standard/base-types/composite-formatting.md)。

- [内插字符串](../tokens/interpolated.md).

有关详细信息，请参阅[标准数值格式字符串](../../../standard/base-types/standard-numeric-format-strings.md)。

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [类型引用表](reference-tables-for-types.md)
- [格式设置类型](../../../standard/base-types/formatting-types.md)
- [复合格式设置](../../../standard/base-types/composite-formatting.md)
- [字符串内插](../tokens/interpolated.md)
- [string](string.md)
