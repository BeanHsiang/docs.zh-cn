---
title: LINQ（语言集成查询）
description: 了解 LINQ 如何向 C# 和 VB 中提供语言级查询功能和 API，以便能够编写具有表达力度的声明性代码。
author: cartermp
ms.author: wiwagn
ms.date: 06/20/2016
ms.technology: dotnet-standard
ms.assetid: c00939e1-59e3-4e61-8fe9-08ad6b3f1295
ms.openlocfilehash: eb1ba14bbcfe4e561fa575b9802126fab59d31fc
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56968025"
---
# <a name="linq-language-integrated-query"></a>LINQ（语言集成查询）

## <a name="what-is-it"></a>什么是 LINQ？

LINQ 在 C# 和 VB 中提供语言级查询功能和[高阶函数](https://en.wikipedia.org/wiki/Higher-order_function) API，以便能够编写具有很高表达力度的声明性代码。

语言级查询语法：

```csharp
var linqExperts = from p in programmers
                  where p.IsNewToLINQ
                  select new LINQExpert(p);
```

同一个示例使用 `IEnumerable<T>` API 的情况：

```csharp
var linqExperts = programmers.Where(p => p.IsNewToLINQ)
                             .Select(p => new LINQExpert(p));
```

## <a name="linq-is-expressive"></a>LINQ 具有很高的表达力度

假设你有一份宠物列表，但想要将它转换为字典，以便可以使用宠物的 `RFID` 值直接访问宠物信息。

传统的命令性代码：

```csharp
var petLookup = new Dictionary<int, Pet>();

foreach (var pet in pets)
{
    petLookup.Add(pet.RFID, pet);
}
```

代码的意图不是创建新的 `Dictionary<int, Pet>` 并通过循环在其中添加条目，而是将现有列表转换为字典！ LINQ 维持这种意图，而命令性代码则不会。

等效的 LINQ 表达式：

```csharp
var petLookup = pets.ToDictionary(pet => pet.RFID);
```

使用 LINQ 的代码非常有效，因为在程序员的推理过程中，LINQ 能够在意图与代码之间找到合理的平衡。 另一个好处就是精简代码。 想像一下，如果能够像上面一样将大部分的基本代码减掉 1/3，情况会怎样？ 很爽，对吧？

## <a name="linq-providers-simplify-data-access"></a>LINQ 提供程序简化数据访问

对于生产环境中的软件，其重要功能块的任务不外乎就是来自某些源（数据库、JSON、XML 等）的数据。 通常，这就需要用户学习每个数据源的新 API，而这是一个枯燥的过程。 LINQ 可将用于数据访问的常用元素抽象化成查询语法，不过你选择哪种数据源，这种语法看上去都是相同的，因而简化了此任务。

考虑以下操作：查找具有特定属性值的所有 XML 元素。

```csharp
public static IEnumerable<XElement> FindAllElementsWithAttribute(XElement documentRoot, string elementName,
                                           string attributeName, string value)
{
    return from el in documentRoot.Elements(elementName)
           where (string)el.Element(attributeName) == value
           select el;
}
```

为了执行此任务而编写代码来手动遍历 XML 文档会带来重重困难。

LINQ 提供程序的作用不仅仅是与 XML 交互。 [Linq to SQL](../../docs/framework/data/adonet/sql/linq/index.md) 是适用于 MSSQL Server 数据库的极其简练的对象关系映射器 (ORM)。 使用 [JSON.NET](https://www.newtonsoft.com/json/help/html/LINQtoJSON.htm) 库可以通过 LINQ 有效遍历 JSON 文档。 此外，如果没有哪个库可以解决你的需要，你还可以[编写自己的 LINQ 提供程序](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2012/bb546158(v=vs.110))！

## <a name="why-use-the-query-syntax"></a>为何使用查询语法？

这是用户经常提出的一个问题。 毕竟，下面的代码

```csharp
var filteredItems = myItems.Where(item => item.Foo);
```

要比下面的代码简洁得多：

```csharp
var filteredItems = from item in myItems
                    where item.Foo
                    select item;
```

难道 API 语法不比查询语法更简洁吗？

不是。 查询语法允许使用 **let** 子句，这样，便可以在表达式的作用域内引入和绑定变量，然后在表达式的后续片段中使用该变量。 只使用 API 语法重现相同的代码也是可行的，不过，这很可能会导致代码难以阅读。

那么，问题来了，**只使用查询语法可以吗？**

在以下情况下，此问题的答案是**可以**...

*   现有的基本代码已使用查询语法
*   由于复杂性的问题，需要在查询中限定变量的作用域
*   你偏好使用查询语法，并且它不会使基本代码变得混乱

在以下情况下，此问题的答案是**不可以**...

*   现有的基本代码已使用 API 语法
*   不需要在查询中限定变量的作用域
*   你偏好使用 API 语法，并且它不会使基本代码变得混乱

## <a name="essential-samples"></a>重要片段示例

有关 LINQ 示例的完整列表，请访问 [101 个 LINQ 示例](https://code.msdn.microsoft.com/101-LINQ-Samples-3fb9811b)。

下面简单演示了 LINQ 的一些重要片段。 没有办法演示完整的代码，因为 LINQ 提供的功能比此处演示的要多得多。

*   语句构成 - `Where`、`Select` 和 `Aggregate`：

```csharp
// Filtering a list
var germanShepards = dogs.Where(dog => dog.Breed == DogBreed.GermanShepard);

// Using the query syntax
var queryGermanShepards = from dog in dogs
                          where dog.Breed == DogBreed.GermanShepard
                          select dog;

// Mapping a list from type A to type B
var cats = dogs.Select(dog => dog.TurnIntoACat());

// Using the query syntax
var queryCats = from dog in dogs
                select dog.TurnIntoACat();

// Summing the lengths of a set of strings
int seed = 0;
int sumOfStrings = strings.Aggregate(seed, (s1, s2) => s1.Length + s2.Length);
```

*   平展列表的列表：

```csharp
// Transforms the list of kennels into a list of all their dogs.
var allDogsFromKennels = kennels.SelectMany(kennel => kennel.Dogs);
```

*   两个集之间的联合（使用自定义比较运算符）：

```csharp
public class DogHairLengthComparer : IEqualityComparer<Dog>
{
    public bool Equals(Dog a, Dog b)
    {
        if (a == null && b == null)
        {
            return true;
        }
        else if ((a == null && b != null) ||
                 (a != null && b == null))
        {
            return false;
        }
        else
        {
            return a.HairLengthType == b.HairLengthType;
        }
    }

    public int GetHashCode(Dog d)
    {
        // default hashcode is enough here, as these are simple objects.
        return d.GetHashCode();
    }
}

...

// Gets all the short-haired dogs between two different kennels
var allShortHairedDogs = kennel1.Dogs.Union(kennel2.Dogs, new DogHairLengthComparer());
```

*   两个集之间的交集：

```csharp
// Gets the volunteers who spend share time with two humane societies.
var volunteers = humaneSociety1.Volunteers.Intersect(humaneSociety2.Volunteers,
                                                     new VolunteerTimeComparer());
```

*   排序：

```csharp
// Get driving directions, ordering by if it's toll-free before estimated driving time.
var results = DirectionsProcessor.GetDirections(start, end)
              .OrderBy(direction => direction.HasNoTolls)
              .ThenBy(direction => direction.EstimatedTime);
```

*   最后，我们演示一个更高级的示例：确定相同类型的两个实例的属性值是否相等（该示例摘自[此 StackOverflow 文章](https://stackoverflow.com/a/844855)，不过已做修改）：

```csharp
public static bool PublicInstancePropertiesEqual<T>(this T self, T to, params string[] ignore) where T : class
{
    if (self == null || to == null)
    {
        return self == to;
    }
    
    // Selects the properties which have unequal values into a sequence of those properties.
    var unequalProperties = from property in typeof(T).GetProperties(BindingFlags.Public | BindingFlags.Instance)
                            where !ignore.Contains(property.Name)
                            let selfValue = property.GetValue(self, null)
                            let toValue = property.GetValue(to, null)
                            where !Equals(selfValue, toValue)
                            select property;
    return !unequalProperties.Any();
}
```

## <a name="plinq"></a>PLINQ

PLINQ（又称并行 LINQ）是 LINQ 表达式的并行执行引擎。 换言之，LINQ 正则表达式可能会没有意义地在任意数量的线程之间并行化。 为此，可以调用表达式前面的 `AsParallel()`。

考虑以下情况：

```csharp
public static string GetAllFacebookUserLikesMessage(IEnumerable<FacebookUser> facebookUsers)
{
    var seed = default(UInt64);

    Func<UInt64, UInt64, UInt64> threadAccumulator = (t1, t2) => t1 + t2;
    Func<UInt64, UInt64, UInt64> threadResultAccumulator = (t1, t2) => t1 + t2;
    Func<Uint64, string> resultSelector = total => $"Facebook has {total} likes!";

    return facebookUsers.AsParallel()
                        .Aggregate(seed, threadAccumulator, threadResultAccumulator, resultSelector);
}
```

此代码将会根据需要在系统线程之间将 `facebookUsers` 分区，累加每个并行线程上的类似项总计，累加每个线程计算的结果，然后将该结果投影为一个合理的字符串。

图示：

![PLINQ 图示](./media/using-linq/plinq-diagram.png)

可通过 LINQ 能够轻松表达的可并行化 CPU 密集型作业（即，没有副作用的纯函数）非常适合使用 PLINQ 来处理。 对于_确实_有副作用的作业，请考虑使用[任务并行库](./parallel-programming/task-parallel-library-tpl.md)。

## <a name="further-resources"></a>其他资源：

*   [101 LINQ 示例](https://code.msdn.microsoft.com/101-LINQ-Samples-3fb9811b)
*   [Linqpad](https://www.linqpad.net/)，适用于 C#/F#/VB 的演练环境和数据库查询引擎
*   [EduLinq](https://codeblog.jonskeet.uk/2011/02/23/reimplementing-linq-to-objects-part-45-conclusion-and-list-of-posts/)，帮助用户了解如何实现 LINQ 到对象的电子书
