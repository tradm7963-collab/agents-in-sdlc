---
title: "练习 5：迭代改进 GitHub Copilot 的工作"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：管理智能体][previous-lesson] |
|:--|

## 审查工作成果

在整个实验中，你与 GitHub Copilot 协作完成了多项任务，以改善用户体验并添加功能。你让 Copilot 为代码添加文档、为设计团队构建可迭代的相关游戏功能，以及实现包括高对比度和浅色模式开关在内的无障碍功能。现在检查代码更改；必要时向 Copilot 提供反馈，改进其工作成果。

### 场景

如前所述，引入生成式 AI 并不会改变软件设计和 DevOps 的基本原则。我们始终需要审查生成的代码，并遵循正常的 DevOps 流程。因此，在为团队其他成员启用审查之前，先审查 GitHub Copilot 建议的文档、相关游戏功能和无障碍功能。

## 安全与 GitHub Copilot 云智能体

由于 Copilot 云智能体会在无人监督的情况下异步执行任务，因此设置了一些安全限制，确保整个过程安全：

- Copilot 只有仓库的读取权限，并且**只能**写入用于执行任务的分支。
- 云智能体在 GitHub Actions 中运行，会创建独立的临时环境来工作。
- GitHub Actions 工作流必须经过人工批准后才能运行。
- 默认情况下，[对外部资源的访问受到限制](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall)，MCP 服务器也包括在内。

## 审查生成的文档

先查看 GitHub Copilot 云智能体创建的第一个拉取请求（PR）：为代码添加文档。通过 GitHub.com 上的标准 PR 界面完成审查。

> [!NOTE]
> 查看 PR 时，可能会看到 GitHub Copilot 被防火墙阻止的警告。这是**预期行为**，因为 Copilot 默认只能有限访问外部资源，包括外部 MCP 服务器调用。你也可以[自定义或禁用 Copilot 云智能体防火墙][agent-firewall]。

1. 返回 github.com 上的仓库。
2. 选择 **Pull Requests**，打开拉取请求列表。
3. 打开标题类似 **Add missing documentation** 的拉取请求。

> [!NOTE]
> 如果 Copilot 仍在处理任务，PR 中会显示 **[WIP]** 标记。此时请等待 Copilot 完成工作。这可能需要几分钟，可以休息一下或回顾目前学到的内容。

4. PR 准备就绪后，选择 **Files changed** 选项卡并审查更改。

    ![Files changed（已更改文件）选项卡](../../../_images/shared-pr-files-changed.png)

5. 查看新添加了 TSDoc 文档注释及其他文档的代码。具体更改会因实际结果而异。

   浏览更改时，留意 TSDoc 文档注释、TypeScript 规范和注释头。这些要求来自你在练习 2 开始时查看的自定义指令文件。

6. 审查更新并确认符合预期后，返回 **Conversation** 选项卡并向下滚动。
7. 查看是否有等待批准的工作流指示器。
8. 如果有等待批准的工作流，选择 **Approve and run workflows**。

   ![Approve and run workflows（批准并运行工作流）](../../../_images/shared-approve-workflows.png)

9. 工作流应会进入拉取请求的检查列表。如果一切正常，单体 Astro 应用的项目检查就会通过。这可能需要几分钟。

## 请求 GitHub Copilot 修改

与 Copilot 协作并不是单向的。你可以像在 PR 中提及其他团队成员一样，在评论或代码内联评论中提及 Copilot。Copilot 会读取这些评论，并启动另一个会话来处理请求。由于结果具有非确定性，我们无法规定必须提出的具体内容。你可以要求 Copilot 更新以下内容：

- 在每个代码文件顶部添加简要说明用途的注释头。
- 为 TypeScript 和 Astro 文件添加 TSDoc 文档注释。
- 创建 README，介绍 Astro 应用的结构。

1. 添加评论请求 Copilot 修改生成的文档，像提及其他用户一样提及 **@copilot**。可以使用上面的任一建议，也可以提出其他文档改进请求。
2. 选择 **View Session** 查看 Copilot 如何执行任务。留意 Copilot 会启动新会话来进行更新。
3. 可以选择 **Back to pull request** 返回拉取请求。

    ![Back to pull request（返回拉取请求）](../../../_images/ex7-back-to-pr.png)

4. Copilot 完成更改后，拉取请求中应会出现新提交。
5. 选择 **Files changed** 选项卡审查更改。

你可以继续迭代，直到满意为止。完成后，可以将 PR 从草稿转换为待审查状态，再合并到主分支。

![将 PR 转为可审查状态](../../../_images/ex7-ready-for-review.png)

## 审查相关游戏功能

现在查看 Copilot 为解决“在游戏详情页显示相关游戏”议题而创建的 PR。

1. 返回 GitHub.com 上的仓库。
2. 选择 **Pull Requests** 选项卡。
3. 选择标题类似 **Show related games on the game details page** 的 PR。
4. 选择 **Files changed** 选项卡，审查生成的代码。
5. 审查更改并确认符合预期后，返回 **Conversation** 选项卡并向下滚动。
6. 查看是否有等待批准的工作流指示器。
7. 如果有等待批准的工作流，选择 **Approve and run workflows**。

   ![Approve and run workflows（批准并运行工作流）](../../../_images/shared-approve-workflows.png)

8. 工作流应会进入 PR 的检查列表。如果一切正常，单体 Astro 应用的项目检查就会通过。这可能需要几分钟。
9. **可选：**也可以在 Codespace 中切换到该分支，手动测试相关游戏功能。转到 Codespace，打开终端并运行以下命令（将 `<branch-name>` 替换为 Copilot 创建的分支名称，例如 **copilot/fix-8**）：

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

Copilot 已构建相关游戏功能！和之前一样，可以通过迭代让云智能体进一步更新。例如，可以要求 Copilot 调整显示的相关游戏数量，或添加注释头和 TSDoc 文档注释（请记住，分配该议题时，指令尚未更新！）。和之前一样，可以在 **Conversation** 选项卡中添加评论请求修改；Copilot 会读取评论并启动新会话。

## 审查无障碍功能

最后，审查由无障碍自定义智能体实现的无障碍功能。此 PR 应同时包含练习 3 中分配的高对比度模式，以及练习 4 在任务控制中心要求添加的浅色模式。

1. 返回 GitHub.com 上的仓库。
2. 选择 **Pull Requests** 选项卡。
3. 选择标题类似 **Add high contrast mode to website** 的 PR。

> [!NOTE]
> 如果 Copilot 仍在处理任务，拉取请求中会显示 **[WIP]** 标记。请等待 Copilot 完成，这可能需要几分钟。

4. 选择 **Files changed** 选项卡，审查生成的代码。
5. 审查实现时，重点留意：
   - 用于切换模式的 UI 组件。
   - 使用本地存储持久化用户偏好。
   - 高对比度和浅色模式的 CSS 或样式更改。
   - 无障碍属性（ARIA 标签、键盘导航等）。
   - 管理模式切换的 JavaScript/TypeScript 代码。

6. 审查更改并确认符合预期后，返回 **Conversation** 选项卡并向下滚动。
7. 查看是否有等待批准的工作流指示器。
8. 如果有等待批准的工作流，选择 **Approve and run workflows**。

   ![Approve and run workflows（批准并运行工作流）](../../../_images/shared-approve-workflows.png)

9. 工作流应会进入 PR 的检查列表。如果一切正常，单体 Astro 应用的项目检查就会通过。这可能需要几分钟。
10. **可选：**可以在 Codespace 中切换到该分支，手动测试无障碍功能。转到 Codespace，打开终端并运行以下命令（将 `<branch-name>` 替换为 Copilot 创建的分支名称）：

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    然后启动应用，在浏览器中测试高对比度和浅色模式开关，确认功能正常，并且刷新页面后设置仍然保留。

留意无障碍自定义智能体如何引导 Copilot 遵循无障碍最佳实践实现功能。如果发现无障碍问题或改进点，可以像前面一样在评论中提及 **@copilot** 请求更新。

## 可选练习——继续委派工作

云智能体最适合处理真实待办事项，让你能同时处理其他任务。可以在自己的仓库中再创建一些议题并分配给 Copilot，练习这种工作方式。可以考虑：

- 在游戏详情页添加支持者意向表单。
- 为游戏列表页添加分页。
- 为数据访问辅助函数添加输入验证和错误处理。

## 总结

你已完成云智能体工作流。通过这些课程，你：

- **检查了仓库附带的自定义指令文件**，以便稍后观察它们对云智能体输出的影响。
- **将议题分配给 Copilot 云智能体**，观察它准备环境、规划并异步执行任务。
- **创建并使用无障碍自定义智能体**，添加高对比度和浅色模式开关。
- **使用 Copilot 智能体页面作为任务控制中心**，监控并引导正在进行的无障碍会话。
- **审查并迭代改进云智能体的拉取请求**，通过提及 `@copilot` 请求修改并批准工作流。

## 回顾和后续步骤

你已完成云智能体工作流。若想继续学习，其他工作流可以补充本次练习的内容：

- 🖥️ **[VS Code 工作流](../../vscode/)** —— 在 IDE 中探索 Copilot Chat 智能体模式和 MCP 集成。
- 💻 **[CLI 工作流](../../cli/)** —— 在终端交付两项经过审查的更改，同时学习 Plan 和 Autopilot 模式、智能体技能、自定义 QA 智能体、Playwright MCP、Agent Merge，以及可选的 `/delegate` 云智能体桥接功能。

在自己的仓库中，还可以尝试以下后续任务：

- 将重构或测试覆盖率议题分配给云智能体。
- 为其他领域创建自定义智能体。
- 为其他技术栈设置 `copilot-setup-steps.yml`。

## 资源

- [GitHub Copilot][github-copilot]
- [关于 Copilot 智能体][copilot-agents]
- [将 GitHub 议题分配给 Copilot][assign-issue]
- [Copilot 云智能体设置工作流最佳实践][cloud-agent-best-practices]
- [配置 Copilot 云智能体防火墙][agent-firewall]

---

| [← 上一课：管理智能体][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
