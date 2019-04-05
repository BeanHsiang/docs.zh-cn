---
title: 机器学习任务 - ML.NET
description: 浏览 ML.NET 中支持的不同机器学习任务和关联的任务。
ms.custom: seodec18
ms.date: 01/15/2019
author: jralexander
ms.openlocfilehash: 02b454d18eca36c94c27ae15665af5df2ec87905
ms.sourcegitcommit: b56d59ad42140d277f2acbd003b74d655fdbc9f1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2019
ms.locfileid: "54415697"
---
# <a name="machine-learning-tasks-in-mlnet"></a>ML.NET 中的机器学习任务

在生成机器学习模型时，首先需要定义你希望通过数据实现的目标。 之后，可以根据你的实际情况选取正确的机器学习任务。 下面介绍了可以从中选择的不同机器学习任务，以及一些常见用例。

> [!NOTE]
> ML.NET 当前处于预览状态。 目前并不支持所有机器学习任务。 若要提交请求以获取某项任务，请在 [dotnet/machinelearning 存储库](https://github.com/dotnet/machinelearning/issues)中打开一个问题。

## <a name="binary-classification"></a>二元分类

[监管式机器学习](glossary.md#supervised-machine-learning)任务，用于预测数据实例所属的两个类（类别）。 分类算法输入是一组标记示例，其中每个标签为整数 0 或 1。 二元分类算法的输出是一个分类器，可用于预测未标记的新实例的类。 二元分类方案示例包括：

* [了解 Twitter 评论的情绪](../tutorials/sentiment-analysis.md)，“正面”或“负面”。
* 诊断患者是否患有某种疾病。
* 决定是否要将电子邮件标记为“垃圾邮件”。
* 确定照片是否包含狗或水果。

有关详细信息，请参阅 Wikipedia 上的[二元分类](https://en.wikipedia.org/wiki/Binary_classification)一文。

推荐的二元分类学习器：

* AveragedPerceptronTrainer
* StochasticGradientDescentClassificationTrainer
* LightGbmBinaryTrainer
* FastTreeBinaryClassificationTrainer
* SymSgdClassificationTrainer

### <a name="binary-classification-learners"></a>二元分类学习器

以下学习器可用于二元分类任务：

* [AveragedPerceptronTrainer](xref:Microsoft.ML.Trainers.Online.AveragedPerceptronTrainer)
* [BinaryClassificationGamTrainer](xref:Microsoft.ML.Trainers.FastTree.BinaryClassificationGamTrainer)
* [FastForestClassification](xref:Microsoft.ML.Trainers.FastTree.FastForestClassification)
* [FastTreeBinaryClassificationTrainer](xref:Microsoft.ML.Trainers.FastTree.FastTreeBinaryClassificationTrainer)
* [FieldAwareFactorizationMachineTrainer](xref:Microsoft.ML.FactorizationMachine.FieldAwareFactorizationMachineTrainer)
* [LightGbmBinaryTrainer](xref:Microsoft.ML.LightGBM.LightGbmBinaryTrainer)
* [LinearSvmTrainer](xref:Microsoft.ML.Trainers.Online.LinearSvmTrainer)
* [LogisticRegression](xref:Microsoft.ML.Learners.LogisticRegression)
* [PriorTrainer](xref:Microsoft.ML.Trainers.PriorTrainer)
* [RandomTrainer](xref:Microsoft.ML.Trainers.RandomTrainer)
* [StochasticGradientDescentClassificationTrainer](xref:Microsoft.ML.Trainers.StochasticGradientDescentClassificationTrainer)
* [SymSgdClassificationTrainer](xref:Microsoft.ML.Trainers.SymSgd.SymSgdClassificationTrainer)

## <a name="multiclass-classification"></a>多类分类

[监管式机器学习](glossary.md#supervised-machine-learning)任务，用于预测数据实例的类（类别）。 分类算法输入是一组标记示例。 每个标签通常以文本形式开始。 然后通过 TermTransform 运行，它可将其转换为 Key（数字）类型。 分类算法的输出是一个分类器，可用于预测未标记的新实例的类。 多类分类方案示例包括：

* 确定狗的品种是“西伯利亚哈士奇”、“金毛寻回犬”、“贵宾犬”等。
* 了解电影评论是“正面”、“中立”还是“负面”。
* 将酒店评语分类为“位置”、“价格”、“整洁度”等。

有关详细信息，请参阅 Wikipedia 上的[多类分类](https://en.wikipedia.org/wiki/Multiclass_classification)一文。

推荐的多类学习器：

* OVA-AveragedPerceptronTrainer
* SdcaMultiClassTrainer
* LightGbmMulticlassTrainer
* OVA-FastTreeBinaryClassificationTrainer

>[!NOTE]
>OVA 和 PKPD 升级任何[二元分类学习器](#binary-classification)，以便对多类数据集进行操作。 有关详细信息，请参阅 [Wikipedia] (https://en.wikipedia.org/wiki/Multiclass_classification#One-vs.-rest)。

### <a name="multiclass-classification-learners"></a>多类分类学习器

以下学习器可用于多类分类任务：

* [LightGbmMulticlassTrainer](xref:Microsoft.ML.LightGBM.LightGbmMulticlassTrainer)
* [MetaMulticlassTrainer<TTransformer,TModel>](xref:Microsoft.ML.Learners.MetaMulticlassTrainer%602)
* [MultiClassNaiveBayesTrainer](xref:Microsoft.ML.Trainers.MultiClassNaiveBayesTrainer)
* [Ova](xref:Microsoft.ML.Trainers.Ova)
* [Pkpd](xref:Microsoft.ML.Trainers.Pkpd)
* [SdcaMultiClassTrainer](xref:Microsoft.ML.Trainers.SdcaMultiClassTrainer)

## <a name="regression"></a>回归

[监管式机器学习](glossary.md#supervised-machine-learning)任务，用于从一组相关特征中预测标签值。 标签可以是任何实际值，而不是像在分类任务中那样来自一组有限的值。 回归算法模拟其相关特征上的标签依赖关系，以确定标签将如何随着特征值的变化而变化。 回归算法输入是一组带已知值标签的示例。 回归算法输出是一个函数，可用于预测任何一组新输入特征的标签值。 回归方案示例包括：

* 基于房子特性（如卧室数量、位置或大小）来预测房价。
* 基于历史数据和当前市场趋势预测将来的股票价格。
* 基于广告预算预测产品销售。

推荐的回归学习器：

* FastTreeTweedieTrainer 
* LightGbmRegressorTrainer 
* SdcaRegressionTrainer 
* FastTreeRegressionTrainer

### <a name="regression-learners"></a>回归学习器

以下学习器可用于回归任务：

* [FastTreeRegressionTrainer](xref:Microsoft.ML.Trainers.FastTree.FastTreeRegressionTrainer)
* [FastTreeTweedieTrainer](xref:Microsoft.ML.Trainers.FastTree.FastTreeTweedieTrainer)
* [LightGbmRegressorTrainer](xref:Microsoft.ML.LightGBM.LightGbmRegressorTrainer)
* [OlsLinearRegressionTrainer](xref:Microsoft.ML.Trainers.HalLearners.OlsLinearRegressionTrainer)
* [OnlineGradientDescentTrainer](xref:Microsoft.ML.Trainers.Online.OnlineGradientDescentTrainer)
* [PoissonRegression](xref:Microsoft.ML.Trainers.PoissonRegression)
* [RegressionGamTrainer](xref:Microsoft.ML.Trainers.FastTree.RegressionGamTrainer)
* [SdcaRegressionTrainer](xref:Microsoft.ML.Trainers.SdcaRegressionTrainer)
* [FastTree.SingleTrainer](xref:Microsoft.ML.Trainers.FastTree.SingleTrainer)
* [LightGBM.SingleTrainer](xref:Microsoft.ML.LightGBM.SingleTrainer)

## <a name="clustering"></a>聚类分析

[非监管式机器学习](glossary.md#unsupervised-machine-learning)任务，用于将数据实例分组到包含类似特性的群集。 聚类分析还可用来识别可能无法通过浏览或简单的观察以逻辑方式推导出的数据集中的关系。 聚类分析算法的输入和输出取决于选择的方法。 可以采取分发、质心、连接或基于密度的方法。 ML.NET 当前支持使用 K 平均值聚类分析的基于质心的方法。 聚类分析方案示例包括：

* 基于酒店选择的习惯和特征来了解酒店来宾群。
* 确定客户群和人口统计信息来帮助生成目标广告活动。
* 基于生产指标对清单进行分类。

### <a name="clustering-learners"></a>聚类分析学习器

以下学习器可用于聚类分析任务：

* [KMeansPlusPlusTrainer](xref:Microsoft.ML.Trainers.KMeans.KMeansPlusPlusTrainer)

## <a name="anomaly-detection"></a>异常情况检测

此任务使用主体组件分析 (PCA) 创建异常情况检测模型。 基于 PCA 的异常情况检测有助于在以下场景中构建模型：可以很轻松地从一个类中获得定型数据（例如有效事务），但难以获得目标异常的足够示例。

PCA 是机器学习中已建立的一种技术，由于它揭示了数据的内部结构，并解释了数据中的差异，因此经常被用于探索性数据分析。 PCA 的工作方式是通过分析包含多个变量的数据。 它查找变量之间的关联性，并确定最能捕捉结果差异的值的组合。 这些组合的特性值用于创建一个更紧凑的特性空间，称为主体组件。

异常情况检测包含机器学习中的许多重要任务：

* 识别潜在的欺诈交易。
* 指示发生了网络入侵的学习模式。
* 发现异常的患者群集。
* 检查输入系统的值。

根据定义，异常情况属于罕见事件，因此很难收集具有代表性的数据样本用于建模。 此类别中包含的算法是专门设计用来解决使用不平衡数据集建立和定型模型的核心挑战。

### <a name="anomaly-detection-learners"></a>异常情况检测学习器

以下学习器可用于异常情况检测任务：

* [RandomizedPcaTrainer](xref:Microsoft.ML.Trainers.PCA.RandomizedPcaTrainer)

## <a name="ranking"></a>排名

排名任务从一组标记的示例构建排名程序。 该示例集由实例组组成，这些实例组可以使用给定的标准进行评分。 每个实例的排名标签是 { 0, 1, 2, 3, 4 }。  排名程序定型为用每个实例的未知分数对新实例组进行排名。 ML.NET 排名学习器基于[机器已学习的排名](https://en.wikipedia.org/wiki/Learning_to_rank)。

### <a name="ranking-learners"></a>排名学习器

以下学习器可用于排名任务：

* [FastTreeRankingTrainer](xref:Microsoft.ML.Trainers.FastTree.FastTreeRankingTrainer)
* [LightGbmRankingTrainer](xref:Microsoft.ML.LightGBM.LightGbmRankingTrainer)

## <a name="recommendation"></a>建议

推荐任务支持生成推荐产品或服务的列表。 ML.NET 使用[矩阵因子分解 (MF)](https://en.wikipedia.org/wiki/Matrix_factorization_%28recommender_systems%29)，这是一种[协作筛选](https://en.wikipedia.org/wiki/Collaborative_filtering)算法，当目录中有历史产品评级数据时，推荐使用该算法。 例如，你为用户提供历史电影评级数据，并希望向他们推荐接下来可能观看的其他电影。

### <a name="recommendation-learners"></a>推荐学习器

以下学习器可用于推荐任务：

* [MatrixFactorizationTrainer](xref:Microsoft.ML.Trainers.MatrixFactorizationTrainer)
* [MatrixFactorizationPredictionTransformer](xref:Microsoft.ML.Trainers.Recommender.MatrixFactorizationPredictionTransformer)
