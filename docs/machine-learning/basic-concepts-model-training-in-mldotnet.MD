---
title: ML.NET 中模型定型的基本概念
description: 本文介绍与 ML.NET 中模型定型方案相关的基本概念。 并非所有观念均与更简单的方案“使用现有模型预测”相关。
ms.date: 03/05/2019
ms.topic: overview
ms.custom: mvc
ms.openlocfilehash: 78554cfd1dfdb3dba82a325d47245aeb313bb6fe
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57675558"
---
# <a name="basic-concepts-for-model-training-in-mlnet"></a>ML.NET 中模型定型的基本概念

本文介绍与 ML.NET 中模型定型方案相关的基本概念。 并非所有观念均与更简单的方案“使用现有模型预测”相关。

本文和相关示例目前使用的是 ML.NET 版本 0.10。 有关详细信息，请参阅 [dotnet/machinelearning GitHub 存储库](https://github.com/dotnet/machinelearning/tree/master/docs/release-notes)上的发行说明。

## <a name="model-training-concepts"></a>模型定型概念

本文档介绍与 ML.NET 中模型定型相关的以下概念：

- [数据](#data)表示为 `IDataView` 接口。
  - 在 ML.NET 中，数据类似于 SQL 视图：它是延迟评估的、不可变的、可应用游标的、异源的架构化数据集。 
  - 可参阅有关数据接口的精彩文档 [IDataView 设计原则](https://github.com/dotnet/machinelearning/blob/master/docs/code/IDataViewDesignPrinciples.md)。
- [转换器](#transformer)表示为 `ITransformer` 接口。
  - 转换器是一种组件，它提取数据，对其执行某些操作，然后返回转换后的新数据。
  - 例如，可以将机器学习模型视为转换器，用于提取特征并返回预测数据。
  - 再举一个例子，文本 tokenizer 提取单个文本列，并输出矢量列，包含从文本中提取出来的单个字词。
- [数据读取器](#data-reader)表示为 `IDataReader<T>` 接口。
  - 数据读取器是用于创建数据的 ML.NET 组件。 它采用 `T` 的实例，并返回其中的数据。 
  - 例如，TextLoader 是一个 `IDataReader<IMultiStreamSource>`。 它提取源，然后产生数据。 
- [估算器](#estimator)表示为 `IEstimator<T>` 接口。
  - 这是学习数据的对象。 学习的结果是转换器。
  - 可将机器学习算法视为估算器，依赖数据进行学习并生成机器学习模型。
- [预测函数](#prediction-function)表示为 `PredictionEngine<TSrc, TDst>` 类。
  - 可将预测函数视为一个向某个行应用转换器的计算机（例如在预测时）。

## <a name="data"></a>数据

在 ML.NET 中，数据类似于 SQL 视图：它是延迟评估的、可应用游标的、异源的架构化数据集。

- 它具有架构（`ISchema` 接口的实例），其中包含数据视图列的相关信息。
  - 每列均包含“名称”、“类型”和与之相关联的任意元数据集。
  - 列的元数据包含矢量列槽名称等信息。 元数据本身表示为另一个单行数据，该数据对每一个列是唯一的。
  - 数据视图是游标的源。 回想一下 SQL 游标：游标是一个对象，它循环访问数据，一次一行，且表示可用数据。
  - 正常情况下，数据可根据需要，具有尽可能多的活动游标。 由于数据本身是不可变的，因此游标是独立的。
  - 游标通常只访问列的子集：为提高效率，ML.NET 只计算游标需要的列的值。

## <a name="transformer"></a>转换器

转换器是一种组件，它提取数据，对其执行某些操作，然后返回转换后的新数据。

ML.NET 中的大多数转换器往往一次操作一个输入列，然后生成输出列。 例如，`new HashTransformer("bar", "foo")` 采用列“foo”中的值，对其进行哈希操作，然后将其放到“bar”列。 

输入列和输出列名称相同是很常见的。 在这种情况下，旧的列被替换为新的列。 例如，`new HashTransformer("foo")` 采用列“foo”中的值，对其进行哈希操作，然后将其放到“foo”。 

如果调用 `Transform`，任何转换器都会生成新的数据视图。 请记住，数据视图是不可变的。

另一个重要的考虑因素是，由于数据评估延迟，转换器也会延迟。 本质上讲，调用之后

```csharp
var newData = transformer.Transform(oldData)
```

未发生任何实际计算。 仅当通过 `newData` 获得游标并开始使用值时，`newData` 才会调用 `transformer` 转换逻辑（甚至是仅在需要 `transformer` 才能生成请求的列的情况下）。

### <a name="transformer-chains"></a>转换器链

转换器有一个有用的属性，是用户可以将一系列转换器的整个应用序列构建为另一个转换器：

```csharp
var fullTransformer = transformer1.Append(transformer2).Append(transformer3);
```

此属性通常在 ML.NET 中使用：通常情况下，定型的 ML.NET 模型就是一个转换器链，对于所有要实现的用途和目的，它就是一个转换器。

## <a name="data-reader"></a>数据读取器

数据读取器是用于“创建”数据的 ML.NET 组件：它采用 `T` 的实例并返回相关数据。

需要注意的一个有趣属性是，可以通过将转换器附加到现有数据读取器，来创建一个数据读取器。 这样便可获得包含转换行为的读取器：

```csharp
var newReader = reader.Append(transformer1).Append(transformer2)
```

与转换器的另一个相似之处是，由于数据评估延迟，读取器也延迟：调用 `reader.Read()` 后未发生任何（或最小程度的）实际“读取”：仅当生成的数据请求游标时，读取器才开始工作。

## <a name="estimator"></a>估算器

估算器是学习数据的对象。 学习的结果是转换器。

在 ML.NET 中，使用此属性创建将不同估算器链接在一起的学习管道：

```csharp
MLContext mlContext = new MLContext(seed: 0);

var pipeline = mlContext.Transforms.CopyColumns("Label","FareAmount")
    .Append(mlContext.Transforms.Categorical.OneHotEncoding("VendorId"))
    .Append(mlContext.Transforms.Categorical.OneHotEncoding("RateCode"))
    .Append(mlContext.Transforms.Categorical.OneHotEncoding("PaymentType"))
    .Append(mlContext.Transforms.Concatenate("Features","VendorId","RateCode","PassengerCount","TripTime","TripDistance","PaymentType"))
    .Append(mlContext.Regression.Trainers.FastTree("Label","Features"));

var model = pipeline.Fit(dataView);
```

估算器的一个重要属性是“估算器积极，无惰性”：每个 `Fit` 调用都会导致学习行为，操作可能会很耗时。

## <a name="prediction-function"></a>预测函数

可将预测函数视为向某行应用转换器的组件。

获取模型（通过 `Fit()` 定型或从其他位置加载的转换器）后，可通过 `model.Transform(data)` 的常规调用，使用模型进行预测。 然而，在实际情景中使用此模型时，通常没有多少可用来进行预测的示例。 往往一次只有一个示例，且需要立即通过示例进行及时预测。

当然，可将此缩减为批预测：

- 创建只有一行的数据视图。
- 调用 `model.Transform(data)` 以获取预测的数据视图。
- 获取生成数据上的游标。
- 将游标移动一步，到达第一（且唯一）行。
- 从其中提取预测值。

可使用[架构理解](https://github.com/dotnet/machinelearning/blob/master/docs/code/SchemaComprehension.md)，通过两个用户定义的对象（`InputExample` 和 `OutputPrediction`）实现上述算法，如下所示：

```csharp
var inputData = mlContext.Data.ReadFromEnumerable(new InputExample[] { example });
var outputData = model.Transform(inputData);
var output = mlContext.CreateEnumerable<OutputPrediction>(outputData,reuseRowObject:false).First();
```

但这很麻烦，并会产生性能成本。 而预测函数对象可通过扩展方法 `CreatePredictionEngine` 执行相同的操作，但速度更快、更方便：

```csharp
var predictionEngine = model.CreatePredictionEngine<InputExample,OutputPrediction>(mlContext);
var prediction = predictionEngine.Predict(example);
```

预测函数是不可重入的/线程安全的。 如果想要使用多个线程同时进行预测，每个线程都需要有一个预测函数。
