---
title: SOA 应用程序
description: 请记住容器也可以是 SOA 应用程序的有用的部署选项。
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 02/15/2019
ms.openlocfilehash: ee71873ac15246f979fd2b08d92280ba797ff6ee
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57675792"
---
# <a name="service-oriented-applications"></a>面向服务的应用程序

面向服务的体系结构 (SOA) 是一个使用过度的术语，意味着不同的人很多不同的理解。 但相同的理解，SOA 意味着通过分解为可进行分类等子系统的不同类型中，或在其他情况下，作为层的多个服务 （通常为 HTTP 服务） 构建的应用程序体系结构。

现在，可以将这些服务部署为 Docker 容器，解决与部署相关的问题，因为容器映像中包含了所有依赖项。 但是，当您需要向外扩展 Soa，如果要部署基于单个实例可能遇到难题。 可以使用 Docker 群集软件或业务流程协调程序处理这一挑战。 我们将探讨微服务方法时，我们来看看下一节中更详细地业务流程协调程序。

对于传统的面向服务的体系结构和更高级的微服务体系结构，Docker 容器都是有用的（但不是必需的）。

在一天结束时，容器聚类分析解决方案是适用于这两种传统 SOA 的体系结构以及在其中每个微服务拥有它的数据模型的更高级的微服务体系结构。 和得益于多个数据库，您还可以向外扩展而不是使用共享的 SOA 服务的整体式数据库的数据层。 但是，有关将数据拆分的讨论是纯粹有关体系结构和设计。

>[!div class="step-by-step"]
>[上一页](state-and-data-in-docker-applications.md)
>[下一页](orchestrate-high-scalability-availability.md)
