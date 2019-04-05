---
title: 在传统 Web 应用和单页应用之间选择
description: 了解在生成 Web 应用时，如何在传统 Web 应用和单页应用程序 (SPA) 之间进行选择。
author: ardalis
ms.author: wiwagn
ms.date: 01/30/2019
ms.openlocfilehash: 5b8569f2abd5160fa8a080c06441a963fb455f6b
ms.sourcegitcommit: 3500c4845f96a91a438a02ef2c6b4eef45a5e2af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/07/2019
ms.locfileid: "55825740"
---
# <a name="choose-between-traditional-web-apps-and-single-page-apps-spas"></a>在传统 Web 应用和单页应用 (SPA) 之间选择

> “Atwood 定律：任何能够用 JavaScript 编写的应用程序，最终必将用 JavaScript 编写。”  
> \- Jeff Atwood

目前可通过两种通用方法来构建 Web 应用程序：在服务器上执行大部分应用程序逻辑的传统 Web 应用程序，以及在 Web 浏览器中执行大部分用户界面逻辑的单页应用程序 (SPA)，后者主要使用 Web API 与 Web 服务器通信。 也可以将两种方法混合使用，最简单的方法是在更大型的传统 Web 应用程序中承载一个或多个丰富 SPA 类子应用程序。

何时应使用传统 Web 应用程序：

- 应用程序的客户端要求简单，甚至要求只读。

- 应用程序需在不支持 JavaScript 的浏览器中工作。

- 团队不熟悉 JavaScript 或 TypeScript 开发技术。

何时应使用 SPA：

- 应用程序必须公开具有许多功能的丰富用户界面。

- 团队熟悉 JavaScript 和/或 TypeScript 开发。

- 应用程序已为其他（内部或公共）客户端公开 API。

此外，SPA 框架还需要更强的体系结构和安全专业知识。 相较于传统 Web 应用程序，SPA 框架需要进行频繁的更新和使用新框架，因此改动更大。 相较于传统 Web 应用，SPA 应用程序在配置自动化生成和部署过程以及利用部署选项（如容器）方面的难度更大。

使用 SPA 模型改进用户体验时必须权衡这些注意事项。

## <a name="razor-components"></a>Razor 组件

ASP.NET Core 3.0 引入了一种新模型，用于构建称为 Razor 组件的丰富的、交互式和可组合的 UI。 Razor 组件允许开发者在服务器上使用 Razor 构建 UI，并使用名为 WebAssembly 的 JavaScript 库将此代码传递到浏览器和执行客户端。 ASP.NET Core 3.0 仍在开发中，但你应该会期望在本电子书的 3.0 更新中看到有关此技术的详细信息。 有关 Razor 组件（名为 Blazor 的代码）的详细信息，请参阅 [Blazor 入门](https://blazor.net/docs/get-started.html)。

## <a name="when-to-choose-traditional-web-apps"></a>何时选择传统 Web 应用

以下内容详细介绍前面提到的选择传统 Web 应用程序的原因。

**应用程序的客户端要求简单，可能要求只读**

对许多 Web 应用程序而言，其大部分用户的主要使用方式是只读。 只读（或以读取为主）应用程序往往比那些维护和操作大量状态的应用程序简单得多。 例如，搜索引擎可能由一个带有文本框的入口点和用于显示搜索结果的第二页组成。 匿名用户可以轻松提出请求，并且很少需要使用客户端逻辑。 同样，一般而言，博客或内容管理系统中面向公众的应用程序主要包含的内容与客户端行为关系不大。 此类应用程序容易构建为基于服务器的传统 Web 应用程序，在 Web 服务器上执行逻辑，并呈现要在浏览器中显示的 HTML。 事实上，网站的每个独特页面都有自己的 URL，搜索引擎可以将其存为书签和编入索引（默认设置，无需将其添加为应用程序的单独功能），这也是此类情况的一个明显优势。

**应用程序需在不支持 JavaScript 的浏览器中工作**

如需在有限或不支持 JavaScript 的浏览器中工作的 Web 应用程序，则应使用传统的 Web 应用工作流编写（或至少可以回退到此类行为）。 SPA 需要客户端 JavaScript 才能正常工作；如果没有客户端 JavaScript，SPA 不是好的选择。

**团队不熟悉 JavaScript 或 TypeScript 开发技术**

如果团队不熟悉 JavaScript 或 TypeScript，但熟悉服务器端 Web 应用程序开发，那相较于 SPA，他们交付传统 Web 应用的速度可能更快。 除非以学习 SPA 编程为目的，或需要 SPA 提供用户体验，否则对已经熟悉构建传统 Web 应用的团队而言，选择传统 Web 应用的工作效率更高。

## <a name="when-to-choose-spas"></a>何时选择 SPA

以下内容详细介绍何时为 Web 应用选择单页应用程序开发样式。

**应用程序必须公开具有许多功能的丰富用户界面**

SPA 可支持丰富客户端功能，当用户执行操作或在应用的各区域间导航时无需重新加载页面。 SPA 很少需要重新加载整个页面，因此加载速度更快，可在后台提取数据，并且对单个用户操作的响应更快。 SPA 支持增量更新，可保存尚未完成的窗体或文档，而无需用户单击按钮提交窗体。 SPA 支持丰富的客户端行为，例如拖放，比传统应用程序更容易操作。 可以将 SPA 设计为在断开连接的模式下运行，对客户端模型进行更新，并在重新建立连接后将更新最终同步回服务器。 如果应用要求包括丰富的功能，且超出了典型 HTML 窗体提供的功能，则应选择 SPA 样式应用程序。

请注意，SPA 通常需要实现内置于传统 Web 应用中的功能，例如在反映当前操作的地址栏中显示有意义的 URL（并允许用户将此 URL 存为书签或对其进行深层链接以便返回此 URL）。 SPA 还应允许用户使用浏览器的后退和前进按钮寻找用户意料之中的结果。

**团队熟悉 JavaScript 和/或 TypeScript 开发**

编写 SPA 需要熟悉 JavaScript 和/或 TypeScript 以及客户端编程技术和库。 团队应有能力像使用 Angular 一样使用 SPA 框架编写新式 JavaScript。

> ### <a name="references--spa-frameworks"></a>参考 - SPA 框架
>
> - **Angular**  
>   <https://angular.io>
> - **JavaScript 框架的比较**  
>   <https://jsreport.io/the-ultimate-guide-to-javascript-frameworks/>

**应用程序已为其他（内部或公共）客户端公开 API**

如果已提供一个 Web API 供其他客户端使用，则相较于在服务器端窗体中复制逻辑，创建一个利用这些 API 的 SPA 实现更加容易。 用户与应用程序交互时，SPA 广泛使用 Web API 来查询和更新数据。

## <a name="decision-table--traditional-web-or-spa"></a>决策表 - 传统 Web 或 SPA

下面的决策表总结了在传统 Web 应用程序和 SPA 之间进行选择时要考虑的一些基本因素。

| **因素**                                           | **传统 Web 应用** | **单页面应用程序** |
| ---------------------------------------------------- | ----------------------- | --------------------------- |
| 需要团队熟悉 JavaScript/TypeScript | **最低**             | **必需**                |
| 支持不带脚本的浏览器                   | **支持**           | **不支持**           |
| 客户端应用程序行为极少             | **适合**         | **不必要**                |
| 丰富而复杂的用户界面要求            | **受限**             | **适合**             |

>[!div class="step-by-step"]
>[上一页](modern-web-applications-characteristics.md)
>[下一页](architectural-principles.md)
