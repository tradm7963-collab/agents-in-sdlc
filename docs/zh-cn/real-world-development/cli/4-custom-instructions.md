---
title: "第 4 课 - 使用自定义指令引导 Copilot"
description: "了解仓库指令、添加文档规范，并将其应用于筛选功能代码。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

使用生成式 AI 时，上下文至关重要。如果任务必须以特定方式完成，就要让 Copilot 能够获取相应指导。[指令文件][instruction-files]不仅说明你想要什么代码，也说明代码应该如何组织。现在你已经构建了筛选功能，接下来将探索 Copilot 使用的指令、添加文档规范，并将其应用于代码。

本课将介绍如何：

- 了解仓库指令和按路径限定的指令文件如何传递给智能体。
- 更新指令文件，确保遵循编码规范。
- 观察指令文件对代码的影响。

## 场景

Tailspin Toys 和其他优秀的开发团队一样，有一套开发实践指南和要求，包括：

- 注释应解释意图和不明显的决策，而不是复述代码。
- `db/` 和 `src/lib/` 中导出的函数应使用 TSDoc/JSDoc 说明用途、参数和返回值；如果有可注入的 `db` 参数，也要说明。
- 可复用的 Astro 组件应记录其 `Props` 接口约定；相关代码更改时，注释也应保持更新。
- 保留现有格式和 lint 指南。

使用指令文件，可以确保 Copilot 了解这些实践要求，并据此完成任务。

## 指令文件

自定义指令可以向 Copilot 提供上下文和偏好，帮助它理解你的编码风格和要求。它可以引导 Copilot 提供更符合需求的建议和代码片段。你可以为整个仓库创建指令，也可以针对特定文件类型创建指令。

指令文件有两种：

- `.github/copilot-instructions.md` 是一个指令文件，会随仓库的**每个**请求发送给 Copilot。文件中应包含适用于大多数请求的项目级信息。
- `.github/instructions/*.instructions.md` 文件用于针对特定语言、文件类型或任务提供指导。

> [!NOTE]
> 其他指令格式及其支持情况会因环境而异。依赖某种格式前，请查阅[自定义指令支持参考][custom-instructions-support]。

## 查看项目中的自定义指令文件

先了解项目中已有的指令文件，再进行修改，以便观察更改的影响。

1. 返回 Codespace。
2. 在 Codespaces 编辑器（而非终端）中打开 `.github/copilot-instructions.md`。
3. 浏览文件，了解项目简介和编码指导。此文件适用于仓库中与 Copilot 的所有交互。
4. 打开 `.github/instructions` 文件夹并查看其中的文件，包括 Astro 文件、Drizzle 数据层、测试等相关指令。
5. 打开 `.github/instructions/unit-tests.instructions.md`。留意顶部的 `applyTo` 字段，它指定了这些指令适用的 glob。
6. 打开 `.github/instructions/drizzle.instructions.md`，查看它对其他指令文件和项目现有文件的链接。这样可以将较大的指令集拆分成可复用的小文件，并提供示例供 Copilot 参考。

## 更新指令以符合团队规范

现有文件已经打下良好基础，但仍缺少一项指导。修改核心 `copilot-instructions.md` 文件，确保新生成的 TypeScript 代码包含 TSDoc 注释。

1. 在 `.github/copilot-instructions.md` 中找到 **Code formatting guidance** 部分，大约位于第 35 行。
2. 在该部分末尾添加以下项目：

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

文件会自动保存！

## 应用更新后的指导

Copilot CLI 会在对话启动时加载仓库指令。保存更新后的指令后，退出并恢复筛选功能会话，以便 Copilot 在保留功能上下文的同时加载新指导。

1. 如果筛选功能会话仍处于打开状态，输入 `/exit` 关闭它。Copilot CLI 会自动保存会话。
2. 在仓库根目录的 `game-filters-cli` 分支上恢复已保存的会话：

   ```bash
   copilot --resume
   ```

   如果出现提示，选择筛选功能会话，并确认当前检出的是 `game-filters-cli` 分支。
3. 让 Copilot 应用更新后的指导：

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. 输入 `/diff`，检查更改的 TypeScript 文件。留意新生成的 TSDoc 注释，并确认其准确说明了代码。

## 总结和后续步骤

你探索了 Copilot CLI 如何读取指令文件中的上下文，并将新的规范应用于功能。具体来说，你：

- 了解仓库指令和按路径限定的指令文件如何传递给智能体。
- 更新了指令文件，确保遵循编码规范。
- 观察了指令文件对代码的影响。

接下来，[自定义并运行可复用的 quality-checks 技能][next-lesson]，确保一致地运行 lint 和测试。

## 资源

- [为 Copilot CLI 添加自定义指令][instruction-files]
- [自定义指令支持][custom-instructions-support]
- [创建自定义指令的最佳实践][instructions-best-practices]
- [Awesome Copilot：指令文件及其他资源集合][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
