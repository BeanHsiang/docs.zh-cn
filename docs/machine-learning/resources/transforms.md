---
title: 机器学习数据转换 - ML.NET
description: 了解在 ML.NET 中受支持的特征工程组件。
author: JRAlexander
ms.custom: seodec18
ms.date: 01/14/2019
ms.openlocfilehash: e649c9a27f0409cb9cdfb554963b5c0e732991f2
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57355399"
---
# <a name="machine-learning-data-transforms---mlnet"></a>机器学习数据转换 - ML.NET

下表包含在 ML.NET 中受支持的数据转换的所有信息。

> [!NOTE]
> ML.NET 当前处于预览状态。 当前并不支持所有数据转换。 要提交某项转换请求，请在 [dotnet/machinelearning](https://github.com/dotnet/machinelearning/issues) GitHub 存储库中发起一个问题。

## <a name="combiners-and-segregators"></a>合并器和分离器

| Transform | 定义 |
| --- | --- |
| <xref:Microsoft.ML.Transforms.GroupTransform> | 根据相邻的组 ID，将标量列的值汇集到矢量中。 |
| <xref:Microsoft.ML.Transforms.UngroupTransform> | 将矢量列取消组合为一系列行；组转换的逆向。 |

## <a name="conversions"></a>转换

| Transform | 定义 |
| --- | --- |
| <xref:Microsoft.ML.Transforms.Conversions.HashingTransformer> | 哈希为单值列或矢量列。 对于矢量列，它分别散列每个槽。 它可以散列文本值或键值。 |
| <xref:Microsoft.ML.Transforms.Conversions.HashJoiningTransform> | 将多个列值转换为哈希。 此转换接受数字和文本输入，包括单值和矢量值列。 |
| <xref:Microsoft.ML.Transforms.Conversions.KeyToBinaryVectorMappingTransformer> | 将键转换为二进制矢量列。 |
| <xref:Microsoft.ML.Transforms.Conversions.KeyToValueMappingTransformer > | 利用 KeyValues 元数据将键索引映射到 KeyValues 元数据中的相应值。 |
| <xref:Microsoft.ML.Transforms.Conversions.KeyToVectorMappingTransformer> | 将键转换为矢量列。 |
| <xref:Microsoft.ML.Transforms.Conversions.TypeConvertingTransformer> | 如果可以转换类型，则更改基础列类型。 |
| <xref:Microsoft.ML.Transforms.Conversions.ValueToKeyMappingTransformer> | 将输入值（单词、数字等）转换为字典中的索引。 |

## <a name="deep-learning"></a>深度学习

| Transform | 定义 |
| --- | --- |
| <xref:Microsoft.ML.Transforms.OnnxTransform> | 为现有 ONNX 模型提供数据并返回分数（预测）。 |
| <xref:Microsoft.ML.Transforms.TensorFlowTransform> | 可以使用预定型的 TensorFlow 模型进行评分或重新定型 TensorFlow 模型。 |

## <a name="feature-extraction"></a>特征提取

| Transform | 定义 |
| --- | --- |
| <xref:Microsoft.ML.Transforms.Text.CustomStopWordsRemovingTransform> | 通过将单个令牌（比较不区分大小写）与非索引字进行比较，删除指定的非索引字列表。|
| <xref:Microsoft.ML.ImageAnalytics.ImageGrayscaleTransform> | 获取一个或多个 ImageType 列，并将其转换为同一图像的灰度表示形式。|
| <xref:Microsoft.ML.ImageAnalytics.ImageLoaderTransform> | 获取一个或多个 ReadOnlyMemory 列，并将其作为 ImageType 加载。 |
| <xref:Microsoft.ML.ImageAnalytics.ImagePixelExtractorTransform> | 获取一个或多个 ImageType 列，并将其转换为矢量表示形式。|
| <xref:Microsoft.ML.ImageAnalytics.ImageResizerTransform> | 采用一个或多个 ImageType 列，并将其大小调整为提供的高度和宽度。|
| <xref:Microsoft.ML.Transforms.Text.LatentDirichletAllocationTransformer> | 实现 LightLDA，这是潜在狄利克雷分布的最先进的实现。|
| <xref:Microsoft.ML.Transforms.LoadTransform> | 从指定的模型文件加载特定转换。 允许从序列化链中挑选转换，或将预定型的转换应用于不同（但仍然符合）的数据视图。 |
| <xref:Microsoft.ML.Transforms.Text.NgramExtractingTransformer> | 在给定的键矢量中生成一组 ngrams 计数（长度为 1-n 的连续值的序列）。 它通过生成 ngram 字典并使用字典中的 ID 作为包中的索引来实现。 |
| <xref:Microsoft.ML.Transforms.Text.NgramExtractorTransform> | 将标记化文本（ReadOnlyMemory 的矢量）或键矢量的集合转换为数字特征矢量。 特征矢量是 ngrams 的计数（长度为 1-n 的连续令牌、单词或键的序列）。 |
| <xref:Microsoft.ML.Transforms.Text.NgramHashExtractingTransformer> | 使用哈希代码将标记化文本（ReadOnlyMemory 的矢量）集合转换为数字特征矢量。 |
| <xref:Microsoft.ML.Transforms.Text.NgramHashingTransformer> | 在给定的文本中生成一组 ngrams 计数（长度为 1-n 的连续单词的序列）。 |
| <xref:Microsoft.ML.Transforms.Categorical.OneHotEncodingTransformer> | 通过基于数据生成类别字典并使用字典中的 ID 作为数组中的索引，将分类值转换为指标数组 |
| <xref:Microsoft.ML.Transforms.Projections.PcaTransform> | 计算特征矢量到低秩子空间的投影。 |
| <xref:Microsoft.ML.Transforms.Text.SentimentAnalyzingTransformer> | 使用预先训练的情绪模型对输入字符串进行评分。 |
| <xref:Microsoft.ML.Transforms.Text.StopWordsRemovingTransformer> | 通过将单个令牌（比较不区分大小写）与非索引字进行比较，以删除特定语言的非索引字列表（最常见的单词）。 |
| <xref:Microsoft.ML.Transforms.Text.WordBagBuildingTransformer> | 在给定的文本中生成一组 ngrams 计数（连续单词的序列）。 它通过生成 ngram 字典并使用字典中的 ID 作为包中的索引来实现。 |
| <xref:Microsoft.ML.Transforms.Text.WordHashBagProducingTransformer> | 在给定的文本中生成一组 ngrams 计数（长度为 1-n 的连续单词的序列）。 它通过散列每个 ngram 并使用哈希值作为包中的索引来实现。 |
| <xref:Microsoft.ML.Transforms.Text.WordTokenizingTransformer> | 使用分隔符字符将文本拆分成单词。 |


## <a name="image-model-featurizers"></a>图像模型特征器

| Transform | 定义 |
| --- | --- |
| <xref:Microsoft.ML.Transforms.AlexNetExtension> | 这是与 <xref:Microsoft.ML.Transforms.DnnImageFeaturizerEstimator> 一起使用的扩展方法，以便使用预定型的 [AlexNet](https://en.wikipedia.org/wiki/AlexNet) 模型。 包含此扩展的 NuGet 还保证包含二进制模型文件。 |
| <xref:Microsoft.ML.Transforms.ResNet18Extension> | 这是与 <xref:Microsoft.ML.Transforms.DnnImageFeaturizerEstimator> 一起使用的扩展方法，以使用预定型的 ResNet18 模型。 包含此扩展的 NuGet 还保证包含二进制模型文件。 |
| <xref:Microsoft.ML.Transforms.ResNet50Extension> | 这是与 <xref:Microsoft.ML.Transforms.DnnImageFeaturizerEstimator> 一起使用的扩展方法，以使用预定型的 ResNet50 模型。 包含此扩展的 NuGet 还保证包含二进制模型文件。 |
| <xref:Microsoft.ML.Transforms.ResNet101Extension> | 这是与 <xref:Microsoft.ML.Transforms.DnnImageFeaturizerEstimator> 一起使用的扩展方法，以使用预定型的 ResNet101 模型。 包含此扩展的 NuGet 还保证包含二进制模型文件。 |

## <a name="label-parsing"></a>标签分析

| Transform | 定义 |
| --- | --- |
| <xref:Microsoft.ML.Transforms.LabelConvertTransform> |  转换标签。 |
| <xref:Microsoft.ML.Transforms.LabelIndicatorTransform> | 将多类标签重新映射为二进制 True、False 标签，主要用于 OVA。|

## <a name="missing-values"></a>缺失值

| Transform | 定义 |
| --- | --- |
| <xref:Microsoft.ML.Transforms.MissingValueDroppingTransformer> | 删除列中的缺失值。 |
| <xref:Microsoft.ML.Transforms.MissingValueIndicatorTransform> | 创建一个布尔值输出列，其槽数与输入列相同，如果缺少输入列中的值，则输出值为 true。 |
| <xref:Microsoft.ML.Transforms.MissingValueReplacingTransformer> | 通过将缺失值替换为默认值或平均值/最小值/最大值（仅适用于非文本列）来处理缺失值。 |

## <a name="normalization"></a>标准化

| Transform | 定义 |
| --- | --- |
| <xref:Microsoft.ML.Transforms.Projections.LpNormalizingTransformer> | Lp-Norm（矢量/行式）标准化转换。 |
| <xref:Microsoft.ML.Transforms.Normalizers.MeanVarDblAggregator> | 计算矢量值列的均值和方差。 它跟踪当前平均值和 M2（平均值的平方差的总和）、NaNs 的数量和非零元素的数量。 |
| <xref:Microsoft.ML.Transforms.Normalizers.MeanVarSngAggregator> | 计算矢量值列的均值和方差。 它跟踪当前平均值和 M2（平均值的平方差的总和）、NaNs 的数量和非零元素的数量。 |
| <xref:Microsoft.ML.Transforms.Normalizers.MinMaxDblAggregator> | 跟踪矢量值列的最小值、最大值、非稀疏值 (vCount) 和 ProcessValue() 调用 (trainCount) 的数量。 |
| <xref:Microsoft.ML.Transforms.Normalizers.NormalizeTransform> | 标准化特征范围。 |
| <xref:Microsoft.ML.Transforms.Normalizers.NormalizingTransformer> |标准化特征范围。 |

## <a name="onnx"></a>Onnx

| Transform | 定义 |
| --- | --- |
| <xref:Microsoft.ML.Transforms.OnnxTransform> | 对使用 ONNX 标准 v1.2 的预定型 ONNX 模型进行评分 |

## <a name="preprocessing"></a>预处理
| Transform | 定义 |
| --- | --- |
| <xref:Microsoft.ML.Transforms.BootstrapSamplingTransformer> | 近似使用泊松采样的自助采样。 |
| <xref:Microsoft.ML.Transforms.Projections.RandomFourierFeaturizingTransformer> | 生成随机傅立叶特征。 |
| <xref:Microsoft.ML.Transforms.Text.TokenizingByCharactersTransformer> | 面向字符的 tokenizer，其中文本被视为一系列字符。 |
| <xref:Microsoft.ML.Transforms.Projections.VectorWhiteningTransformer> | 简化优化以帮助识别权重。 |

## <a name="row-filters"></a>行筛选器

| Transform | 定义 |
| --- | --- |
| <xref:Microsoft.ML.Transforms.RowShufflingTransformer> | 使用给定行数的池混淆试图执行操作的随机游标。  |
| <xref:Microsoft.ML.Transforms.SkipFilter> | 允许通过跳过多行来将输入限制为行的子集。 |
| <xref:Microsoft.ML.Transforms.SkipTakeFilter> | 允许将输入限制为可选偏移的行的子集。 可用于实现数据分页。 使用 SkipTakeFilter.SkipArguments 创建时，表现为 `SkipFilter`。
| <xref:Microsoft.ML.Transforms.TakeFilter> | 允许通过使用 N 个第一行来将输入限制为行的子集。 |


## <a name="schema"></a>架构

| Transform | 定义 |
| --- | --- |
| <xref:Microsoft.ML.Transforms.ColumnCopyingTransformer> | 复制数据集中的列。|
| <xref:Microsoft.ML.Transforms.ColumnSelectingTransformer> | 选择要从给定输入中删除或保留的一组列。 |
| <xref:Microsoft.ML.Transforms.FeatureSelection.SlotsDroppingTransformer> | 删除列中的槽。|
| <xref:Microsoft.ML.Transforms.OptionalColumnTransform> | 使用指定的类型和默认值创建新列。 |
| <xref:Microsoft.ML.Transforms.RangeFilter> | 在 Single、Double 或 Key 类型的列上筛选数据视图（相邻）。 保留指定的最小/最大范围内的值。 总是筛选出 NaN。如果输入是 Key 类型，则最小值/最大值将被视为值数量的百分比。 |

## <a name="tensorflow"></a>TensorFlow

| Transform | 定义 |
| --- | --- |
| <xref:Microsoft.ML.Transforms.TensorFlowTransform> | 使用预定型的 TensorFlow 模型进行评分或重新定型 TensorFlow 模型。 |

## <a name="text-processing-and-featurization"></a>文本处理和特征化

| Transform | 定义 |
| --- | --- |
| <xref:Microsoft.ML.Transforms.Text.TextNormalizingTransformer> | 文本规范化转换，可以规范化文本大小写、删除标注字符、标点符号和/或数字。 转换对文本输入以及令牌/文本（ReadOnlyMemory 的矢量）的矢量进行的操作。 |
| <xref:Microsoft.ML.Transforms.Text.TokenizingByCharactersTransformer> | 面向字符的 tokenizer，其中文本被视为一系列字符。 |

## <a name="time-series"></a>时序

| Transform | 定义 |
| --- | --- |
| <xref:Microsoft.ML.TimeSeriesProcessing.ExponentialAverageTransform> | 采用值的加权平均值：ExpAvg(y_t) = a * y_t + (1-a) * ExpAvg(y_(t-1))。 |
| <xref:Microsoft.ML.TimeSeriesProcessing.IidChangePointDetector> | 实现 i.i.d 的更改点检测器转换。 基于自适应内核密度估计和鞅的序列（随机样本）。 |
| <xref:Microsoft.ML.TimeSeriesProcessing.IidSpikeDetector> | 实现 i.i.d 的峰值检测器转换。 基于自适应内核密度估计的序列（随机样本）。 |
| <xref:Microsoft.ML.TimeSeriesProcessing.MovingAverageTransform> | 提供滑动窗口值的加权平均值。 |
| <xref:Microsoft.ML.TimeSeriesProcessing.PercentileThresholdTransform> | 确定时序当前值是否属于滑动窗口排在前列的几个值的百分比。 |
| <xref:Microsoft.ML.TimeSeriesProcessing.PValueTransform> | 根据滑动窗口中的其他值计算该系列当前值经验 p 值。 |
| <xref:Microsoft.ML.TimeSeriesProcessing.SlidingWindowTransform> | 在 Single 类型的时序上输出滑动窗口。 |
| <xref:Microsoft.ML.TimeSeriesProcessing.SsaChangePointDetector> | 基于时序的奇异谱建模实现更改点检测器转换。 |
| <xref:Microsoft.ML.TimeSeriesProcessing.SsaSpikeDetector> | 基于时序的奇异谱建模实现峰值检测器转换。 |

## <a name="miscellaneous"></a>杂项

| Transform | 定义 |
| --- | --- |
| <xref:Microsoft.ML.Transforms.CompositeTransformer> | 创建复合 DataTransform。 |
| <xref:Microsoft.ML.Transforms.CustomMappingTransformer%602> | 为提供的 `IDataView` 生成其他列。 它不会更改行数，并且可以看作是将用户的函数应用于输入数据的每一行的结果。|
| <xref:Microsoft.ML.Transforms.GenerateNumberTransform> | 添加具有已生成数字序列的列。 |
| <xref:Microsoft.ML.Transforms.ProduceIdTransform> | 生成以游标的 ID 作为列的列。 |
| <xref:Microsoft.ML.Transforms.RandomNumberGenerator> | 生成随机数。 |
