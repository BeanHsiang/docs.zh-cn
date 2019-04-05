---
title: 布尔运算符
description: 了解有关中可用的布尔运算符F#编程语言。
ms.date: 05/16/2016
ms.openlocfilehash: 5353b6ec6a0bd610f3446761a1d28f01f0403302
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53612733"
---
# <a name="boolean-operators"></a>布尔运算符

本主题介绍中的布尔运算符的支持F#语言。

## <a name="summary-of-boolean-operators"></a>布尔运算符的摘要

下表总结了中可用的布尔运算符F#语言。 这些运算符支持的唯一类型是`bool`类型。

|运算符|描述|
|--------|-----------|
|`not`|布尔值求反|
|<code>&#124;&#124;</code>|布尔 OR|
|`&&`|布尔 AND|

执行布尔 AND 和 OR 运算符*短路计算*，即，它们仅在必要时以确定总体结果表达式的计算运算符右侧的表达式。 第二个表达式`&&`仅当第一个表达式的计算结果为计算运算符`true`; 的第二个表达式`||`仅当第一个表达式的计算结果为计算运算符`false`。

## <a name="see-also"></a>请参阅

- [位运算符](bitwise-operators.md)
- [算术运算符](arithmetic-operators.md)
- [符号和运算符参考](index.md)