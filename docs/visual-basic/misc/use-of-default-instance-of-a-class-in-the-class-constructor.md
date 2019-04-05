---
title: 在类构造函数中使用类的默认实例可能会导致无限递归调用
ms.date: 07/20/2015
ms.assetid: 9645b47f-7de5-46d0-bb45-d5fdaa8aaa2a
ms.openlocfilehash: 14c498bf3067415f8de2afaeaaa57cf3f28ae857
ms.sourcegitcommit: 5c1abeec15fbddcc7dbaa729fabc1f1f29f12045
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2019
ms.locfileid: "58045267"
---
# <a name="use-of-default-instance-of-a-class-in-the-class-constructor-could-lead-to-infinite-recursive-call"></a>在类构造函数中使用类的默认实例可能会导致无限递归调用
已在类的构造函数中使用类的默认实例。 这可能会导致无限递归调用（也称为无限循环）。  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   从类构造函数中删除默认实例。  
  
## <a name="see-also"></a>请参阅

- [构造函数](~/docs/visual-basic/programming-guide/concepts/object-oriented-programming.md#constructors)
