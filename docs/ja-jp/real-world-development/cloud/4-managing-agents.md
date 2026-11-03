---
title: "演習 4 - エージェントの監視と管理"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

前のいくつかの演習では、Copilot cloud agent にユーザー体験の改善と機能追加を目的とする 3 つのタスクを依頼しました。cloud agent は非同期かつ自律的に動作しますが、タスクの進行状況を監視することも重要です。

cloud agent に割り当てたタスクを管理する方法はいくつかあります。[GitHub.com のエージェントページ][agents-page]では、オープンなプルリクエスト (PR) があるすべてのエージェントタスクを確認できます。実行内容を調べたり、進行中のセッションに指示を追加したりできます。

このレッスンでは、次の内容を学習します。

- cloud agent のタスクを監視するために、エージェントページを確認する。
- 進行中のセッションに機能追加を依頼する。

## シナリオ

ハイコントラストモードの作成をエージェントに依頼した後、チームはライトモードも追加するとよいと考えました。サイトのスタイルと切り替え機能を更新する作業を進めているため、ライトモードも含めるのが合理的です。ハイコントラストモードに加えてライトモードも実装するよう、エージェントに指示します。

## Copilot cloud agent のタスクを確認する

Copilot cloud agent に割り当てたすべてのタスクの状態を確認します。

1. [Copilot agents ページ](https://github.com/copilot/agents)を開きます。
2. メインペインと左ペインのタスクリストを確認します。割り当てた次のようなタスクが表示されます。
    - コードベースのドキュメントの更新
    - ゲーム変更用 API の生成
    - Web サイトへのハイコントラストモードの追加
3. 実行中のタスクを選択し、Copilot が実行した作業を確認します。たとえば、次のような操作があります。
    - リポジトリからコードをチェックアウトする
    - Copilot の作業環境を作成する
    - MCP サーバーを設定する
    - 割り当てられたタスクを完了するための手順を実行する

> [!NOTE]
> 表示される手順は、Copilot の作業状況や選択したアプローチによって異なります。

4. 右側に表示されるプルリクエスト (PR) ペインも確認します。ここでは、PR と変更されたファイルを確認できます。

## Cloud agent に指示を追加する

実行中のタスクを確認したので、エージェントがハイコントラストモードを作成している間に、ライトモードも追加するよう依頼します。

1. ハイコントラストモードを追加するセッションを選択します。正確なタイトルは Copilot が付けた名前や作業状況によって異なります。

    ![ミッションコントロールに表示されたアクセシビリティセッション](../../../_images/ex6-accessibility-session.png)

2. セットアップが完了して作業が始まったことを示すメッセージが表示されるまで、数分間セッションを確認します。
3. **Steer active session while Copilot is working** ダイアログに次のプロンプトを入力します。

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![Copilot が作業中のセッションに指示を追加するダイアログが強調表示された、エージェントページのスクリーンショット](../../../_images/ex6-steer-cloud-agent-task.png)

4. <kbd>Enter</kbd> を押してプロンプトを送信します。
5. Copilot がプロンプトを受け取り、作業に取り込むことを確認します。

## Copilot の作業を待つ

Copilot は更新されたタスクに取り組みます。メッセージを送信した時点で実行していた手順が終わると、新しい依頼を作業に取り込みます。

前回と同様に完了まで数分かかります。その間、これまでに学習した内容を振り返りましょう。

## まとめと次のステップ

Copilot cloud agent のタスクを監視し、ガイドするための中心的な場所である Copilot agents ページについて学びました。ここでは、実行中および完了したタスクを追跡し、実行内容を確認して、進行中のタスクに指示を追加できます。

このレッスンでは、次の内容を学習しました。

- ミッションコントロールとエージェントページで cloud agent のタスクを監視する。
- 進行中のセッションに機能追加を依頼する。

Copilot がアクセシビリティ機能に取り組んでいる間に、[Copilot が作成したプルリクエストを改善します][next-lesson]。

## リソース

- [Copilot agents ページ][agents-page]
- [カスタムエージェントについて][custom-agents]

---

| [← 前のレッスン: カスタムエージェント][previous-lesson] | [次のレッスン: Copilot の作業を改善する →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
