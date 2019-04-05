---
title: 在 ML.NET 中使用广义加性模型和形状函数来解释模型
description: 在 ML.NET 中使用广义加性模型和形状函数来解释模型
ms.date: 03/05/2019
ms.custom: mvc,how-to
ms.openlocfilehash: f7b8b9a3daabb16f59c901911a1f6950ce864fff
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57675584"
---
# <a name="use-generalized-additive-models-and-shape-functions-for-model-explainability-in-mlnet"></a>在 ML.NET 中使用广义加性模型和形状函数来解释模型

> [!NOTE]
> 本主题引用 ML.NET（目前处于预览状态），且材料可能会更改。 有关详细信息，请访问 [ML.NET 简介](https://www.microsoft.com/net/learn/apps/machine-learning-and-ai/ml-dotnet)。

此操作说明和相关示例目前使用的是 ML.NET 版本 0.10。 有关详细信息，请参阅 [dotnet/machinelearning GitHub 存储库](https://github.com/dotnet/machinelearning/tree/master/docs/release-notes)上的发行说明。

在创建机器学习模型时，仅仅进行预测通常是不够的。 机器学习开发人员、决策者以及受模型影响的人员通常需要了解机器学习模型如何做出决策，以及哪些特性有助于提高其性能。 广义加性模型 (GAM) 在 Microsoft 内部用于解释模型，帮助机器学习开发人员创建易于由他人解释的高容量模型。

GAM 是一类可解释模型，为线性模型，其中的项是非线性函数，称为单个变量的“形状函数”。 作为线性模型，它们易于解释，但由于模型学习的是特性函数，而不是单一权重，因此它们可以建立比简单线性模型更复杂的关系模型。 生成的 GAM 预测器有一个表示定型集平均预测的截距项，以及表示与平均预测偏差的形状函数。 可目测检查形状函数，以查看模型对某个特性的不同值的响应，并将其可视化，如以下在代码示例结束时创建的图表所示。 ML.NET 中的 GAM 定型程序的实施是使用浅层梯度推进树（例如树桩）来学习非参数形状函数，它基于 Lou、Caruana 和 Gehrke 在[分类和回归的可识别模型](https://www.cs.cornell.edu/~yinlou/papers/lou-kdd12.pdf)中所述的方法。

```csharp
// Train the Generalized Additive Model
var fitPipeline = pipeline.Fit(data);
var gamModel = fitPipeline.LastTransformer.Model;

// The intercept for Generalize Additive Models represent the average prediction for the training data
var intercept = gamModel.Intercept;
Console.WriteLine($"Average predicted cost: {intercept:0.00}");

// Get the column names from the training set
var columnNames = data.Schema.AsEnumerable()
    .Select(column => column.Name) // Get the column names
    .Where(name => name != "MedianHomeValue") // Drop the Label
    .ToArray();

// Get the index of a variable from the training data
var myFeatureIndex = columnNames.ToList().FindIndex(str => str.Equals("MyFeature"));

// The shape functions represent the deviation from the average prediction as a function of the feature value
// It is represented by a discrete set of bins
// First, get the array of bin upper bounds from the model for this feature
var myFeatureBins = gamModel.GetBinUpperBounds(myFeatureIndex);
// Then get the array of bin weights; these are the effect size for each bin
var myFeatureWeights = gamModel.GetBinEffects(myFeatureIndex);

// Write out the shape function for the feature (see the following figure for what this looks like)
for (int i = 0; i < myFeatureBins.Length; i++)
{
    Console.WriteLine($"x < {myFeatureBins[i]:0.00} => {myFeatureWeights[i]:0.000}");
}
```

![广义加性模型形状函数图](./media/use-gams-for-model-explainability/gam-shape-function-graph.png)

有关如何定型 GAM 模型并检查和解释结果的示例，请参阅 [dotnet/machinelearning GitHub 存储库](https://github.com/dotnet/machinelearning/blob/master/docs/samples/Microsoft.ML.Samples/Dynamic/GeneralizedAdditiveModels.cs)。
