---
title: 常用客户端 Web 技术
description: 使用 ASP.NET Core 和 Azure 构建新式 Web 应用程序 | 常用客户端 Web 技术
author: ardalis
ms.author: wiwagn
ms.date: 01/30/2019
ms.openlocfilehash: 36bb18d21740f406d33306c212195fa5dbb25ee1
ms.sourcegitcommit: 3500c4845f96a91a438a02ef2c6b4eef45a5e2af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/07/2019
ms.locfileid: "55828327"
---
# <a name="common-client-side-web-technologies"></a>常用客户端 Web 技术

> “优秀的网站应表里如一。”  
> _- Paul Cookson_

ASP.NET Core 应用程序属于 Web 应用程序，并且通常依赖于 HTML、CSS 和 JavaScript 等客户端 Web 技术。 通过将页面 (HTML) 内容从其布局和样式 (CSS) 以及行为 (JavaScript) 中分离出来，复杂的 Web 应用也可以利用“关注分离”原则。 将来，当这些关注点不相互交织时，可以更轻松地对应用程序的结构、设计或行为进行更改。

尽管 HTML 和 CSS 相对稳定，但应用程序框架和实用程序开发人员用于生成基于 Web 的应用程序的 JavaScript，正以惊人的速度发展。 本章介绍 Web 开发人员在开发应用程序中使用 JavaScript 的几种方式，同时提供有关 Angular 和 React 客户端库的高级概述。

## <a name="html"></a>HTML

HTML（超文本标记语言）是标准标记语言，用于创建网页和 Web 应用程序。 它的元素组成了网页的构建基块，表示格式化文本、图像、窗体输入和其他结构。 浏览器发出 URL 请求时，无论提取网页还是应用程序，首先需要返回 HTML 文档。 这个 HTML 文档可能引用或包括关于其外观、CSS 形式的布局或 JavaScript 形式的行为的详细信息。

## <a name="css"></a>CSS

CSS（级联样式表）用于控制 HTML 元素的外观和布局。 CSS 样式可直接应用于 HTML 元素，单独对相同页面进行定义，或在单独文件中定义或由页面引用。 样式根据用于选择给定 HTML 元素的方式进行级联。 例如，样式可应用于整个文档，但会由应用于特定元素的样式覆盖。 同样，特定于元素的样式会由应用于 CSS 类的样式（曾应用于该元素）覆盖，后者反过来会由指向该元素的特定实例（通过其 ID）的样式覆盖。 图 6-1

**图 6-1**。 按顺序排列的 CSS 特殊性规则。

![](./media/image6-1.png)

最好将样式保存在单独的样式表文件中，并使用基于选择的级联在应用程序内实现一致且可重用的样式。 应避免将样式规则置于 HTML 中，但将样式（而不是规则）应用于特定的各个元素（不是元素的整个类，也不是应用特定 CSS 类的元素）除外。

### <a name="css-preprocessors"></a>CSS 预处理器

CSS 样式表缺少对条件逻辑、变量以及其他编程语言功能的支持。 因此，大型样式表通常包含大量重复，如将相同的颜色、字体或其他设置应用于 HTML 元素和 CSS 类的多个不同的变体。 通过添加对变量和逻辑的支持，CSS 预处理器可帮助样式表遵循 [DRY 原则](https://deviq.com/don-t-repeat-yourself/)。

最常用的 CSS 预处理器是 Sass 和 LESS。 两者均可扩展 CSS 并与其后向兼容，表示无格式 CSS 文件即为有效的 Sass 或 LESS 文件。 Sass 基于 Ruby，而 LESS 基于 JavaScript，二者通常作为本地部署过程的一部分运行。 两者都提供命令行工具，以及 Visual Studio 中的内置支持，可使用 Gulp 或 Grunt 任务运行它们。

## <a name="javascript"></a>JavaScript

JavaScript 是动态的解释性编程语言，已在 ECMAScript 语言规范中进行标准化。 它是 Web 的编程语言。 与 CSS 一样，JavaScript 可定义为 HTML 元素中的属性，作为网页或单独文件中的脚本基块。 正如 CSS，一般建议将 JavaScript 组织到单独的文件中，并尽可能将其与各个网页或应用程序视图中找到的 HTML 分开保存。

在 Web 应用程序中使用 JavaScript 时，通常需要执行以下几项任务：

- 选择 HTML 元素并检索和/或更新其值。

- 查询 Web API 以获取数据。

- 向 Web API 发送命令（并使用其结果响应回叫）。

- 执行验证。

可以仅使用 JavaScript 执行上述所有任务，但存在的许多库可简化这些任务。 其中一个，也是最成功的库是 jQuery，仍是在网页上简化这些任务的热门选择。 对于单页应用程序 (SPA)，jQuery 不会提供 Angular 和 React 提供的众多所需功能。

### <a name="legacy-web-apps-with-jquery"></a>使用 jQuery 的旧版 Web 应用

尽管 jQuery 基于古老的 JavaScript 框架标准，但它仍然是十分常用的库，用于处理 HTML/CSS 和生成对 Web API 进行 AJAX 调用的应用程序。 但是，jQuery 按浏览器文档对象模型 (DOM) 级别操作，并默认只提供命令性，而不是声明性的模型。

例如，假设一个文本框的值超过 10，则应使页面上的元素可见。 在 jQuery 中，此操作通常通过使用检查文本框的值，并根据该值设置目标元素可见性的代码编写事件处理程序来实现。 这是一种基于代码的命令性方法。 另一种框架可能转而使用数据绑定，以声明的方式将元素的可见性与文本框值绑定。 这种方法不需要编写任何代码，改为只需要修饰数据绑定属性涉及的元素。 随着客户端行为变得更加复杂，数据绑定方法经常成为更简单的解决方案，其包含的代码和条件复杂性也较少。

### <a name="jquery-vs-a-spa-framework"></a>jQuery 与 SPA Framework

| **因素** | **jQuery** | **Angular**|
|--------------------------|------------|-------------|
| 抽象 DOM | **是** | **是** |
| AJAX 支持 | **是** | **是** |
| 声明性数据绑定 | **否** | **是** |
| MVC 样式路由 | **否** | **是** |
| 模板化 | **否** | **是** |
| 深层链接路由 | **否** | **是** |

本质上，jQuery 缺少的大多数功能均可通过添加其他库进行添加。 但是，SPA 框架（如 Angular）以更集中的方式提供这些功能，因为它从一开始设计的时候就考虑到了这一点。 此外，jQuery 是一种命令性十分明显的库，这意味着你需要调用 jQuery 函数才能使用 jQuery 执行任何任务。 SPA 框架提供的很多工作和功能都可以声明的方式完成，无需编写任何实际代码。

数据绑定便是一个很好的示例。 在 jQuery 中，通常只需要一个代码行就能获得 DOM 元素的值或设置某元素的值。 但是，你必须在需要更改元素值的任何时候编写此代码，有时，一个页面的多项功能中会发生此情况。 另一常见示例是元素可见性。 在 jQuery 中，可能存在不同的位置，需要编写代码控制特定元素是否可见。 每这两种情况中，如果使用数据绑定，便无需编写任何代码。 只需将元素可见性的值绑定到页面的 viewmodel 即可，对该 viewmodel 做出的任何更改都会自动反映在绑定元素中。

### <a name="angular-spas"></a>Angular SPA

AngularJS 快速成为了世界上最常用的一种 JavaScript 框架。 在 Angular 2 中，团队彻底重建了框架（使用 [TypeScript](https://www.typescriptlang.org/)），并将 AngularJS 重新命名为简单的 Angular。 目前的 Angular 4 版本仍是用于生成单页面应用程序的可靠框架。

Angular 应用程序基于组件构建。 组件通过特殊对象与 HTML 模板进行组合，并控制页面的一部分。 下面是 Angular 文档中的简单组件：

```js
import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `<h1>Hello {{name}}</h1>`
})

export class AppComponent { name = 'Angular'; }
```

组件使用 @Component 修饰器函数定义，可接收有关组件的元数据。 选择器属性可在显示此组件的页面上标识元素的 ID。 模板属性是一个简单的 HTML 模板，包括最后一行上定义的对应于组件名称属性的占位符。

通过使用组件和模板，而不是 DOM 元素，Angular 应用可以更高的抽象级别操作，且比单独使用 JavaScript（也称为“vanilla JS”）或 jQuery 编写的应用具有更少的总体代码。 Angular 还强加了有关如何组织客户端脚本文件的特定顺序。 按照约定，Angular 应用使用常用文件夹结构，同时模块和组件脚本文件位于应用文件夹中。 与生成、部署和测试应用相关的 Angular 脚本通常位于更高级别的文件夹中。

Angular 还可充分利用命令行接口 (CLI) 工具。 从本地入门 Angular 开发（假设已安装 git 和 npm）包括简单地从 GitHub 中克隆存储库以及运行 `npm install` 和 `npm start`。 除此之外，Angular 附带自己的 CLI 工具，可用于创建项目、添加工具，并协助测试、打包和部署任务。 这种 CLI 工具友好性也使 Angular 特别兼容 ASP.NET Core，后者也可提供很好的 CLI 支持。

Microsoft 开发了一个参考应用程序，[eShopOnContainers](https://aka.ms/MicroservicesArchitecture)，其中包含 Angular SPA 实现。 此应用包含 Angular 模块，可用于管理在线商店的购物篮，加载和显示其目录中的商品并处理订单创建。 可以在 [GitHub](https://github.com/dotnet-architecture/eShopOnContainers/tree/master/src/Web/WebSPA) 中查看和下载该示例应用程序。

### <a name="react"></a>React

与 Angular 不同，Angular 提供完整的模型 - 视图 - 控制器模式实现，而 React 仅关注视图。 它不是一个框架，只是一个库，因此需要利用其他库才能生成 SPA。

React 最重要的特征之一是使用虚拟 DOM。 虚拟 DOM 可向 React 提供多项好处，包括性能（虚拟 DOM 可优化实际 DOM 的哪部分需要更新）和可测试性（无需使用浏览器即可测试 React 和它与虚拟 DOM 的交互）。

React 很少使用与 HTML 配合的方式。 React 直接在其 JavaScript 代码中以 JSX 的形式添加 HTML，而没有代码和标记（可能引用 HTML 属性中出现的 JavaScript）之间的严格分离。 JSX 是类似 HTML 的语法，可向下编译为纯 JavaScript。 例如:

```js
<ul>
{ authors.map(author =>
    <li key={author.id}>{author.name}</li>
)}
</ul>
```

如果已了解 JavaScript，学习 React 应该很简单。 与 Angular 或其他常用库相比，它几乎不涉及众多的学习曲线或特殊语法。

由于React 不是完整的框架，因此通常需要其他库来处理路由、Web API 调用和依赖关系管理等任务。 好处是可为每个任务选择最合适的库，但坏处时需要进行所有决策，并在完成后验证所有选定库是否可以很好地协同工作。 如果想要一个好的开端，可使用初学者工具包（如 React Slingshot）,它可使用 React 预先打包一组可兼容库。

### <a name="choosing-a-spa-framework"></a>选择 SPA 框架

考虑哪个 JavaScript 框架最适合支持 SPA 时，请注意以下几项：

- 团队是否熟悉该框架及其依赖关系（某些情况下还包括 TypeScript）？

- 框架的“固执”程度如何，以及是否同意它处理事情的默认方式？

- 它（或伴随库）是否包括应用需要的所有功能？

- 是否有大量文件可查？

- 它在社区中的活跃程度？ 新项目是否使用它生成？

- 它的核心团队活跃程度如何？ 是否定期解决问题和发布新版本？

JavaScript 框架仍以极快的速度发展。 使用上面列出的注意事项，可帮助减轻选择之后会后悔依赖的框架的风险。 如果你特别不愿意承担风险，请考虑提供商业支持和/或大型企业开发的框架。

> ### <a name="references--client-web-technologies"></a>参考 - 客户端 Web 技术
> - **HTML 和 CSS**  
> <https://www.w3.org/standards/webdesign/htmlcss>
> - **Sass 与 LESS**  
> <https://www.keycdn.com/blog/sass-vs-less/>
> - **使用 LESS、Sass 和 Font Awesome 为 ASP.NET Core 应用设置样式**  
> <https://docs.microsoft.com/aspnet/core/client-side/less-sass-fa>
> - **ASP.NET Core 中的客户端开发**  
> <https://docs.microsoft.com/aspnet/core/client-side/>
> - **jQuery**  
> <https://jquery.com/>
> - **jQuery 与 AngularJS**  
> <https://www.airpair.com/angularjs/posts/jquery-angularjs-comparison-migration-walkthrough>
> - **Angular**  
> <https://angular.io/>
> - **React**  
> <https://facebook.github.io/react/>
> - **React Slingshot**  
> <https://github.com/coryhouse/react-slingshot>
> - **React 与 Angular 2 比较**  
> <https://www.codementor.io/codementorteam/react-vs-angular-2-comparison-beginners-guide-lvz5710ha>
> - **2017 年 5 佳 JavaScript 框架**  
> <https://hackernoon.com/5-best-javascript-frameworks-in-2017-7a63b3870282>

>[!div class="step-by-step"]
>[上一页](common-web-application-architectures.md)
>[下一页](develop-asp-net-core-mvc-apps.md)