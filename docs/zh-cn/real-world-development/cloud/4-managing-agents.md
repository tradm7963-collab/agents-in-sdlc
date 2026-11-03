---
title: "练习 4 - 监控和管理智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

在前几个练习中，你让 Copilot 云智能体执行了三项不同任务，以改善用户体验并添加功能。云智能体虽然能够异步自主工作，但监控这些任务仍然很重要。

你可以使用多种工具管理分配给云智能体的任务，包括 GitHub.com 上的[智能体页面][agents-page]。在这个任务控制中心中，可以查看所有拥有未关闭拉取请求（PR）的智能体任务，了解已执行的操作，甚至引导正在进行的会话。

本课将介绍如何：

- 使用智能体页面监控云智能体任务。
- 引导正在进行的会话，要求添加额外功能。

## 场景

将任务分配给智能体以实现高对比度模式后，团队意识到同时添加浅色模式也很合适。既然已经开始更新网站样式并添加切换功能，将这项功能一起实现也很合理。现在引导智能体，要求它除高对比度模式外也添加浅色模式。

## 查看 Copilot 云智能体任务

查看当前分配给 Copilot 云智能体的所有任务的状态。

1. 转到 [Copilot 智能体页面](https://github.com/copilot/agents)。
2. 查看主面板和左侧面板中的任务列表。列表中应包含你分配给 Copilot 的任务，例如：
   - 为代码库添加文档。
   - 生成用于修改游戏的 API。
   - 为网站添加高对比度模式。
3. 选择一个正在运行的任务，查看 Copilot 已执行的工作，例如：
   - 从仓库检出代码。
   - 为 Copilot 创建工作环境。
   - 设置 MCP 服务器。
   - 执行任务所需的各种步骤。

> [!NOTE]
> 所列步骤会根据 Copilot 的工作状态和执行方式而有所不同。

4. 同时留意右侧显示的 PR 面板，可以在其中查看拉取请求和更改的文件，以便进一步监控。

## 引导云智能体

现在已经查看了正在进行的任务，可以让 Copilot 在实现高对比度模式时也添加浅色模式切换开关。

1. 选择与添加高对比度模式相关的会话。具体标题取决于 Copilot 使用的名称和当前工作状态。

    ![任务控制中心中的无障碍会话](../../../_images/ex6-accessibility-session.png)

2. 观察会话几分钟，直到它显示设置已完成并开始执行任务。出现类似以下消息时，就表示已开始工作。
3. 在 **Steer active session while Copilot is working** 对话框中，添加以下提示：

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![智能体页面中突出显示“Steer active session while Copilot is working”对话框的截图](../../../_images/ex6-steer-cloud-agent-task.png)

4. 按 <kbd>Enter</kbd> 发送提示。
5. 留意 Copilot 如何确认收到提示并将它纳入工作流程。

## 让 Copilot 完成工作

和之前一样，Copilot 会继续处理更新后的任务！它会在完成你发送消息时正在执行的具体步骤后，将新请求纳入工作流程。

同样，这需要几分钟。你可以借此暂停一下，回顾目前学到和探索的内容。

## 总结和后续步骤

本课介绍了 Copilot 智能体页面，即监控和引导 GitHub Copilot 云智能体任务的中心位置。你可以使用任务控制中心跟踪所有正在进行和已完成的任务、审查工作，还可以重定向正在进行的任务以调整范围或提供额外指导。

本课中，你了解了：

- 使用任务控制中心和智能体页面监控云智能体任务。
- 重定向正在进行的会话，要求添加额外功能。

Copilot 正在完成无障碍功能，接下来可以[迭代改进它创建的拉取请求][next-lesson]。

## 资源

- [Copilot 智能体页面][agents-page]
- [关于自定义智能体][custom-agents]

---

| [← 上一课：自定义智能体][previous-lesson] | [下一课：迭代改进 Copilot 的工作 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
