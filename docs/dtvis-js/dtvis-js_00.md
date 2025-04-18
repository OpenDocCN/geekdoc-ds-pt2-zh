## 前言

我们越来越无法忽视数据在我们生活中的重要性。数据对人类历史上最大的社会组织至关重要（如 Facebook 和 Google 这样的巨头），而它的收集也具有广泛的地缘政治影响，正如我们在 NSA 监控丑闻中看到的那样。但同样，我们也越来越容易忽视数据本身。一个估计表明，我们系统收集的 99.5% 的数据都被浪费了。

*数据可视化*是解决这一空白的工具。有效的可视化能够澄清问题；它们将抽象的数字集合转化为形状和形式，让观众迅速理解并掌握。这些最佳的可视化能够直观地传达这种理解。观众能够立即理解数据——无需深思。这使得观众能够更充分地考虑数据的含义：它讲述的故事，它揭示的洞察，甚至是它所提供的警告。

如果你今天正在开发网站或 web 应用程序，那么你很可能需要传达数据——这些数据最适合通过良好的可视化呈现。那么，你怎么知道什么样的可视化是合适的呢？更重要的是，如何真正创建一个可视化？在接下来的章节中，我们将探讨数十种不同的可视化方法、技术和工具包。每个例子都会讨论可视化的适用性（并提供可能的替代方案），并提供逐步的指导，帮助你将可视化添加到网页中。

## 本书的理念

在编写本书时，我尝试遵循四个主要原则，以确保它能提供有意义且实用的指导。

+   **实现与设计**

    本书不会教你如何设计数据可视化。老实说，其他一些作者在这方面比我更有资格（比如爱德华·塔夫特）。相反，本书将专注于如何实现可视化。在适当的情况下，我会从更宏观的角度讨论某些可视化策略的优缺点，但主要目标是向你展示如何创建各种可视化。（我知道有时候老板坚决要求做饼图。）

+   **代码与样式**

    正如你从标题中猜到的，这本书专注于如何使用 JavaScript 代码创建可视化。例子并不假设你是 JavaScript 专家——如果遇到比基本 jQuery 选择器更复杂的代码，我会确保为你解释清楚——但是我不会花太多时间讨论可视化的样式。幸运的是，样式化可视化与样式化其他 web 内容基本相同。对 HTML 和 CSS 的基本了解将有助于你将可视化添加到网页中。

+   **简单与复杂**

    书中的大多数示例都是简单、直接的可视化。复杂的可视化可能具有吸引力和说服力，但学习大量的高级代码通常不是学习这项技能的最佳方式。在这些示例中，我会尽量保持简单，这样你就能清晰地看到如何使用各种工具和技术。然而，简单并不意味着无聊，甚至最简单的可视化也可以启发人心、激发灵感。

+   **现实与理想世界的对比**

    当你开始构建自己的可视化时，你会发现现实世界通常并不像你希望的那样友好。开源库可能有 bug，第三方服务器可能存在安全问题，并且并非每个用户都更新到了最新的 Web 浏览器。我在本书的示例中已经解决了这些现实问题。我会向你展示如何在实践中兼容旧版浏览器，如何遵守诸如跨域资源共享（CORS）等安全约束，以及如何绕过他人代码中的 bug。

## 书籍目录

接下来的章节涵盖了各种可视化技术以及我们可以用来实现它们的 JavaScript 库。

+   **第一章** 从最基本的可视化开始——使用 Flotr2 库创建静态图表和绘图。

+   **第二章** 为可视化添加了交互性，用户可以选择内容、放大查看和跟踪值。本章还展示了如何直接从 Web 获取可视化所需的数据。为了多样化，其示例使用了基于 jQuery 的 Flot 库。

+   **第三章** 讨论了如何在网页中整合多个可视化和其他内容；它使用了 jQuery sparklines 库。

+   在 **第四章** 中，我们考虑了除标准图表和绘图外的其他可视化类型，包括树形图、热图、网络图和词云。每个示例都专注于一个特定的 JavaScript 库，该库专为该类型的可视化而设计。

+   **第五章** 涉及基于时间的可视化。本章探讨了几种可视化时间轴的方法，包括传统库、纯 HTML、CSS 和 JavaScript，以及功能全面的 Web 组件。

+   在 **第六章** 中，我们讨论了地理数据，并探讨了将地图整合到可视化中的不同方法。

+   **第七章** 介绍了强大的 D3.js 库，这是一个灵活且功能全面的工具包，用于构建几乎任何类型的自定义可视化。

+   从**第八章**开始，我们将探讨基于 Web 的可视化的其他方面。本章展示了 Underscore.js 库，它使得准备驱动我们可视化的数据变得更加容易。

+   最后，**第九章** 和 **第十章** 详细讲解了一个完整的单页 Web 应用程序的开发，该应用程序依赖于数据可视化。在这里，我们将看到如何使用现代开发工具，如 Yeoman 和 Backbone.js 库。

## 示例的源代码

为了使文本尽可能清晰易读，示例通常包含孤立的 JavaScript 代码片段，以及偶尔的 HTML 或 CSS 片段。所有示例的完整源代码可以在 GitHub 上找到，网址是 *[`jsDataV.is/source/`](http://jsDataV.is/source/)*。
