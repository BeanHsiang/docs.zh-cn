---
title: 可以为 null 的运算符
description: 了解有关中可用的可以为 null 运算符的信息F#编程语言。
ms.date: 05/16/2016
ms.openlocfilehash: b17c0de2d81a1ef88b31d833a49ff9e3f9d34e8d
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53610588"
---
# <a name="nullable-operators"></a>可以为 null 的运算符

可以为 null 的运算符是二元一端或两端使用可以为 null 的算术类型的算术或比较运算符。 使用源如允许使用空值来替代实际值的数据库中的数据时经常会出现可以为 null 的类型。 在查询表达式中通常使用可以为 null 的运算符。 除了可以为 null 的算术运算符和比较运算符，可以使用转换运算符可以为 null 的类型之间进行转换。 也有某些查询运算符的为空版本。

## <a name="table-of-nullable-operators"></a>可以为 Null 的运算符的表

下表列出了可以为 null 的运算符中支持F#语言。

|在左侧可以为 null|右侧可以为 null|双方可以为 null|
|---|---|---|
|[?>=](https://msdn.microsoft.com/library/94d29e32-a204-4f60-a527-6b0af86268f3)|[>=?](https://msdn.microsoft.com/library/0a255d8e-8cae-4160-ae61-243a5d96583f)|[?>=?](https://msdn.microsoft.com/library/3051a50f-d276-4c84-9d73-bf2efeddef94)|
|[?>](https://msdn.microsoft.com/library/62dc0021-1312-4ac3-be87-798b60b81bb6)|[>?](https://msdn.microsoft.com/library/0ad1284b-de48-4a04-83d8-b6f13c9c8936)|[?>?](https://msdn.microsoft.com/library/dc18b6fa-30c4-47b0-9057-794439378a05)|
|[?<=](https://msdn.microsoft.com/library/56fddf0a-e4ca-4891-a3be-fad1876be3b6)|[<=?](https://msdn.microsoft.com/library/02454a0f-30ca-4e77-ad84-ee7837461804)|[?<=?](https://msdn.microsoft.com/library/5c37c28c-0b57-4da5-be11-5a123f7e8ee4)|
|[?<](https://msdn.microsoft.com/library/b71897f0-6e29-4c58-b0a7-a5bfa6f88917)|[<?](https://msdn.microsoft.com/library/be9ea40f-a67f-4e98-8067-a14046752e8b)|[?<?](https://msdn.microsoft.com/library/6f1962c8-5605-468c-94ae-f379ae98e17d)|
|[?=](https://msdn.microsoft.com/library/5cdc8ff6-244b-49cf-9376-69ecf249fd7c)|[=?](https://msdn.microsoft.com/library/d2102894-6a51-475d-890a-735568c31f87)|[?=?](https://msdn.microsoft.com/library/5f793f29-1084-4570-b1c1-17c1b7ef764b)|
|[?<>](https://msdn.microsoft.com/library/3643a5a8-2ea5-4ad6-82c4-83927c3884a0)|[<>?](https://msdn.microsoft.com/library/3179aace-70c4-4911-9258-619592214976)|[?<>?](https://msdn.microsoft.com/library/5da813d8-ee75-45b8-9ef4-146dcb6d394d)|
|[?+](https://msdn.microsoft.com/library/2e8ddd05-b3f3-41b3-9d73-938d9e540f3f)|[+?](https://msdn.microsoft.com/library/74772ea8-f010-493e-bdb5-ba347f2fd4f1)|[?+?](https://msdn.microsoft.com/library/57f28137-0f42-43d2-92af-cad8c6c9d05f)|
|[?-](https://msdn.microsoft.com/library/f237a7a6-89f2-48b2-a2fe-f0b98a2bedc2)|[-?](https://msdn.microsoft.com/library/4a345c07-314a-48f1-b557-ce072583589c)|[?-?](https://msdn.microsoft.com/library/e0024142-1d2a-4607-a39c-1eb1e86fa25a)|
|[?*](https://msdn.microsoft.com/library/519da708-5ad6-4075-9d74-d00441cd6078)|[*?](https://msdn.microsoft.com/library/04c47870-de7b-480d-98a0-f47593b4ffac)|[?*?](https://msdn.microsoft.com/library/e57057ba-9c3a-40ec-8401-150c2b25f75b)|
|[?/](https://msdn.microsoft.com/library/add02a42-f556-40a7-a168-fbf2053322e3)|[/?](https://msdn.microsoft.com/library/1de07646-3778-476d-8c61-5d37495d463c)|[?/?](https://msdn.microsoft.com/library/b17be0ac-bf98-4590-861d-a4dd6c6fa535)|
|[?%](https://msdn.microsoft.com/library/44297bba-1bd9-4ed2-a848-f1e1e598db87)|[%?](https://msdn.microsoft.com/library/a4c178e5-eec4-42e8-847f-90b24fc609fe)|[?%?](https://msdn.microsoft.com/library/dd555f20-1be3-4b8d-81f1-bf1921e62fda)|

## <a name="remarks"></a>备注

中包含的可以为 null 的运算符[NullableOperators](https://msdn.microsoft.com/library/2c3633c5-3f31-4d62-a9f8-272ad6b19007)命名空间中的模块[Microsoft.FSharp.Linq](https://msdn.microsoft.com/library/4765b4e8-4006-4d8c-a405-39c218b3c82d)。 对于可以为 null 的数据类型是`System.Nullable<'T>`。

在查询表达式中，选择从允许空值而不是值的数据源的数据时，会出现可以为 null 的类型。 在 SQL Server 数据库中，表中的每个数据列具有一个属性，指示是否允许 null 值。 如果允许空值，从数据库返回的数据可以包含 null 值的基元数据类型如不能表示`int`， `float`，依次类推。 因此，作为返回的数据`System.Nullable<int>`而不是`int`，并`System.Nullable<float>`而不是`float`。 可以从获取实际值`System.Nullable<'T>`通过使用对象`Value`属性，并且可以确定是否`System.Nullable<'T>`的对象的值通过调用`HasValue`方法。 另一个有用的方法是`System.Nullable<'T>.GetValueOrDefault`方法，让你能够获取的值或默认值为适当的类型。 默认值是某种形式的"零"值，例如 0、 0.0 或`false`。

可能会为 null 的类型转换为不可为 null 的基元类型，如使用常用转换运算符`int`或`float`。 还有可能要从一种可以为 null 的类型转换为另一种可以为 null 的类型，通过使用转换运算符可以为 null 的类型。 适当的转换运算符具有相同的名称作为标准的但它们是在单独的模块， [Nullable](https://msdn.microsoft.com/library/e7a4ea13-28cc-462e-bc3a-33131ace976e)中的模块[Microsoft.FSharp.Linq](https://msdn.microsoft.com/library/4765b4e8-4006-4d8c-a405-39c218b3c82d)命名空间。 通常情况下，使用查询表达式时打开此命名空间。 在这种情况下，可以通过添加前缀使用可以为 null 的转换运算符`Nullable.`到适当的转换运算符，如以下代码所示。

```fsharp
open Microsoft.FSharp.Linq

let nullableInt = new System.Nullable<int>(10)

// Use the Nullable.float conversion operator to convert from one nullable type to another nullable type.
let nullableFloat = Nullable.float nullableInt

// Use the regular non-nullable float operator to convert to a non-nullable float.
printfn "%f" (float nullableFloat)
```

输出为 `10.000000`。

查询运算符可以为 null 的数据字段，如`sumByNullable`，也存在在查询表达式中使用。 不可以为 null 的类型的查询运算符不兼容的类型与 null 的类型，因此使用可以为 null 数据值时，必须使用相应的查询运算符的可以为 null 版本。 有关详细信息，请参阅[查询表达式](../query-expressions.md)。

下面的示例演示如何使用可以为 null 的运算符中的F#查询表达式。 第一个查询显示如何编写查询中不可以为 null 的运算符;第二个查询显示了使用可以为 null 的运算符的等效查询。 有关完整的上下文，包括如何将数据库设置为使用此代码示例，请参阅[演练：使用类型提供程序访问 SQL 数据库](../../tutorials/type-providers/accessing-a-sql-database.md)。

```fsharp
open System
open System.Data
open System.Data.Linq
open Microsoft.FSharp.Data.TypeProviders
open Microsoft.FSharp.Linq

[<Generate>]
type dbSchema = SqlDataConnection<"Data Source=MYSERVER\INSTANCE;Initial Catalog=MyDatabase;Integrated Security=SSPI;">

let db = dbSchema.GetDataContext()

query {
    for row in db.Table2 do
    where (row.TestData1.HasValue && row.TestData1.Value > 2)
    select row
} |> Seq.iter (fun row -> printfn "%d %s" row.TestData1.Value row.Name)

query {
    for row in db.Table2 do
    // Use a nullable operator ?>
    where (row.TestData1 ?> 2)
    select row
} |> Seq.iter (fun row -> printfn "%d %s" (row.TestData1.GetValueOrDefault()) row.Name)
```

## <a name="see-also"></a>请参阅

- [类型提供程序](../../tutorials/type-providers/index.md)
- [查询表达式](../query-expressions.md)