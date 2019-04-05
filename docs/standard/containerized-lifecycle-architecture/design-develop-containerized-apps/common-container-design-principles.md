---
title: 常见容器设计原则
description: 了解很好的容器设计的基本原则，它是一个容器应承载只是一个过程。
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 02/15/2019
ms.openlocfilehash: 206963d63cf8e6ab4fc61b9176f1ba095868c6fc
ms.sourcegitcommit: 2b986afe4ce9e13bbeec929c9737757eb61de60e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/22/2019
ms.locfileid: "56664297"
---
# <a name="common-container-design-principles"></a>常见容器设计原则

提前到开发过程中获取的有几个值得一提的是有关如何使用容器的基本概念。

## <a name="container-equals-a-process"></a>容器等于一个过程

在容器模型中，容器表示单个进程。 通过定义为进程边界的容器，在开始创建到横向，或批处理关闭时，进程使用的基元。 当您运行的 Docker 容器时，您将看到[入口点](https://docs.docker.com/engine/reference/builder/#/entrypoint)定义。 这会定义进程和容器的生存期。 完成后，容器生命周期结束。 有长时间运行的进程，如 web 服务器和生存期较短的进程，例如批处理作业、 已作为 Microsoft Azure 实现[WebJobs](https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/)。 如果进程失败，则容器结束，Orchestrator 接管。 如果业务流程协调程序已指示要保留五个实例运行，并且其中一个出现故障，则 orchestrator 会创建另一个容器来替换失败的进程。 在批处理作业中，使用参数启动该进程。 进程完成，则工作完成。

你可能会发现你希望在单个容器中运行的多个进程的方案。 在任何体系结构文档中，永远不会"从来没有，"也不是始终将"always"。 对于需要多个进程的情况下，一种常见模式是使用[监督程序](http://supervisord.org/)。

>[!div class="step-by-step"]
>[上一页](design-docker-applications.md)
>[下一页](monolithic-applications.md)