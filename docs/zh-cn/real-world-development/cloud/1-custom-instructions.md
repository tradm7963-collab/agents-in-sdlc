---
title: "练习 1 - 自定义指令（云智能体）"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：先决条件][previous-lesson] · [下一课：Copilot 云智能体 →][next-lesson]

使用生成式 AI 时，上下文至关重要。如果任务必须以特定方式完成，或者 Copilot 需要了解一些背景信息，就要确保它能获取这些上下文。[指令文件][instruction-files]用于提供此类指导，帮助 Copilot 理解你想让它做什么以及应该如何完成。

本练习将介绍如何：

- 了解项目上下文、编码指南和文档规范如何通过仓库自定义指令及按路径限定的指令文件传递给 Copilot。
- 向 `.github/copilot-instructions.md` 添加新的仓库级规范。

> [!NOTE]
> 与 VS Code 和 CLI 工作流不同，本练习不会比较更新指令前后的提示结果。Copilot 云智能体会在 GitHub 议题上异步工作，因此难以实时并排展示指令的影响。稍后审查云智能体创建的拉取请求时，你会看到指令文件产生的效果。

## 指令文件

### 场景

Tailspin Toys 和其他优秀的开发团队一样，有一套开发实践指南和要求，包括：

- 数据层始终需要单元测试。
- UI 应采用深色模式并具有现代感。
- 应使用 TSDoc 文档注释为代码添加说明。
- 每个文件开头都应添加注释块，说明该文件的用途。

使用指令文件，可以确保 Copilot 了解这些实践要求，并据此完成任务。

### 自定义指令

自定义指令可以向 Copilot 提供上下文和偏好，帮助它理解你的编码风格和要求。它可以引导 Copilot 提供更符合需求的建议和代码片段。你可以为整个仓库创建指令，也可以针对特定文件类型创建指令。

指令文件有两种：

- `.github/copilot-instructions.md` 是一个指令文件，会随仓库的**每个**请求发送给 Copilot。文件中应包含适用于大多数聊天或 CLI 请求的项目级信息，例如所用技术栈、项目概述、最佳实践和全局指导。
- `.github/instructions/*.instructions.md` 文件可针对特定任务或文件类型提供指导，例如特定编程语言、UI 组件或单元测试。

> [!NOTE]
> 在 IDE 中，指令文件仅用于 Copilot Chat 代码生成，不适用于代码补全或下一步编辑建议。
>
> Copilot Chat、Copilot CLI 和 Copilot 云智能体在生成代码时都会使用仓库级指令和带有 `applyTo` frontmatter 的 `*.instructions.md` 文件。
>
> Copilot 还支持其他标准的指令文件，包括 AGENTS.md 和 CLAUDE.md。

### 管理指令文件的最佳实践

全面介绍如何创建指令文件超出了本研讨会的范围，不过示例项目展示了一种有代表性的做法：

- 在 `copilot-instructions.md` 中集中放置项目级指导，例如项目内容、结构和全局编码规范。
- 使用 `*.instructions.md` 文件为特定文件类型（单元测试、Astro 组件、数据层）或任务提供专门指令。
- 使用自然语言，保持指导清晰，并提供代码应当和不应当采用的示例。

创建指令文件没有唯一正确的方法，使用 AI 也是如此。通过实践可以找到最适合项目的做法。

> [!TIP]
> 每个使用 GitHub Copilot 的项目都应具备一组完善的指令文件。浏览本项目中的文件时，你可能会发现有适用于[界面更新][ui-instructions]和 [Astro][astro-instructions] 等任务的指令。
>
> Copilot 也可以帮助生成指令文件。不同产品界面的操作方式有所不同，例如 VS Code 中的 **Configure Chat → Generate Agent Instructions**，或 Copilot CLI 中的 `/init`。本研讨会会在相关课程中介绍对应操作。
>
> 想寻找模板或入门示例？可以浏览 [awesome-copilot][awesome-copilot]，其中收录了指令文件、自定义智能体和其他资源。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## 查看项目中的自定义指令文件

花些时间查看仓库附带的指令文件：一个核心 `copilot-instructions.md`，以及一组适用于不同任务的 `*.instructions.md` 文件。可以在编辑器或 GitHub 网页界面中打开这些文件。

1. 打开 `.github/copilot-instructions.md`。
2. 浏览项目简介，以及 **Agent notes**、**Code standards**、**Scripts** 和 **Repository Structure** 等部分。留意 **Code standards** 下的 **GitHub Actions Workflows** 指引。这些内容适用于你与 Copilot 的所有交互。
3. 打开 `.github/instructions` 文件夹并查看其中的文件，包括 Astro 文件、Drizzle 数据层、测试等相关指令。
4. 打开 `.github/instructions/unit-tests.instructions.md`。留意顶部的 `applyTo` 字段，它指定了相对于仓库根目录的 glob。此处任何 TypeScript 测试文件（例如匹配 `**/*.test.ts` 的文件）都会应用这些指令。
5. 查看该文件中为项目创建单元测试提供的具体指导。
6. 最后打开 `.github/instructions/drizzle.instructions.md` 并滚动到末尾。留意它对其他指令文件（例如 `unit-tests.instructions.md`）和项目现有文件的链接。这样可以将较大的指令集拆分成可复用的小文件，并提供示例供 Copilot 参考。链接路径相对于指令文件，而非仓库根目录。

> [!NOTE]
> `copilot-instructions.md` 中的 **Code formatting requirements** 部分记录了项目编码规范，但尚未要求提供代码文档。接下来将添加 TSDoc 文档注释和文件注释头的规则。

## 添加新的仓库规范

接下来只需编辑一次：添加一项项目级规则，要求代码使用 TSDoc 文档注释，并在文件开头添加注释头。之后本工作流中，你分配给 Copilot 的议题都会采用这项指令。

编辑前先创建分支（云智能体会读取议题目标分支中的指令，但仍建议干净地提交自己的更改）：

1. 在 codespace 终端中创建并切换到新分支：

   ```bash
   git checkout -b custom-instructions-cloud
   ```

如前所述，`.github/copilot-instructions.md` 用于向 Copilot 提供项目级信息。现在添加一项编码规范，改善代码建议。

1. 重新打开 `.github/copilot-instructions.md`。
2. 找到 **Code formatting requirements** 部分，大约位于第 27 行。留意其中记录了项目的编码规范，但没有代码文档要求，因此之前生成的辅助函数没有文档注释。
3. 在现有规范下方添加以下 Markdown 内容，要求 Copilot 添加文件注释头和 TSDoc 文档注释：

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. 保存 `copilot-instructions.md`。

> [!TIP]
> 如上一课所示，可以在仓库级文件 `.github/copilot-instructions.md` 中定义全局指导，也可以使用 `*.instructions.md` 文件为特定语言、文件类型或任务提供指导。仓库级文件适合放置整个项目都适用的规范，例如刚添加的文档注释规则。

## 提交、推送并合并指令更新

云智能体会读取议题目标分支上的指令。下一练习中分配议题时，Copilot 会从 `main` 创建分支，因此必须先将指令更新合并到 `main`，云智能体才能使用。

1. 暂存并提交更改：

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. 推送分支：

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. 在 github.com 上创建从 `custom-instructions-cloud` 到 `main` 的拉取请求并合并。下一练习中处理分配给云智能体的议题时，它就会读取这些指令。

> [!TIP]
> 如果想在本研讨会中直接使用 `main`，可以跳过分支步骤并直接提交到 `main`。此处创建分支是为了模拟真实项目中的工作方式。

## 总结和后续步骤

你探索了 Copilot 如何读取项目指令文件中的上下文，并向 `.github/copilot-instructions.md` 添加了新的仓库级规范。之后的工作流中，你会看到云智能体创建的拉取请求如何体现这项规范。

接下来，[将首个议题分配给 Copilot 云智能体][next-lesson]。

## 资源

- [GitHub Copilot 自定义指令文件][instruction-files]
- [创建自定义指令的最佳实践][instructions-best-practices]
- [编写更好的 Copilot 自定义指令的 5 个提示][copilot-instructions-five-tips]
- [Awesome Copilot：指令文件及其他资源集合][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
