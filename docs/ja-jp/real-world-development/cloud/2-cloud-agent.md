---
title: "演習 2 - GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: カスタム指示][previous-lesson] |
|:--|

技術的負債に悩まされていない組織は、ほとんどありません。未解決のセキュリティ問題、更新が必要なレガシーコード、実装する時間がなくバックログに残った機能要望など、さまざまな形があります。GitHub Copilot cloud agent は、コードの更新や機能の追加といったタスクを自律的に実行できます。作業が完了すると、人がレビューできるドラフトのプルリクエスト (PR) を作成します。面倒な作業を委任して開発プロセスを加速し、開発者がより大きな課題に集中できるようにします。

この演習では、Copilot cloud agent について次の内容を学習します。

- コード生成環境のカスタマイズ
- 操作を安全に行う方法
- Issue の範囲を明確にする重要性
- Issue を Copilot に割り当てる方法

## シナリオ

Tailspin Toys には解消したい技術的負債があります。最初のサイトを構築した外部委託先が、ドキュメントを適切に残しませんでした。実際には、ドキュメントがほとんどありません。最初の対応として、アプリケーションのエクスポートされたすべての関数に TSDoc ドキュメントコメントを追加します。

また、デザインチームはゲームを見つけやすくしたいと考えています。各ゲームの詳細ページに、同じカテゴリに属するほかのゲームを表示し、閲覧を続けられるようにします。まずはユーザー受け入れテストで UX を試せればよく、仕上げはまだ必要ありません。現在は作業の妨げになっていますが、より優先度の高い Issue もあります。

どちらも、優先度が下がりやすいタスクの例です。Copilot cloud agent に割り当てれば、開発者は別の作業を進め、後から Copilot の変更をレビューできます。

## GitHub Copilot cloud agent について

[GitHub Copilot cloud agent](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) は、人間の開発者と同様に、バックグラウンドでタスクを実行できます。人間の開発者に依頼する場合と同じように、[GitHub Issue を Copilot に割り当てる][assign-issue]方法などで作業を依頼できます。割り当てると、Copilot は進行状況を追跡するドラフト PR を作成し、環境を準備してタスクを開始します。作業中でも完了後でも、Copilot のセッションを確認できます。提案された解決策のレビュー準備ができると、PR でメンションされます。

## 範囲を明確にした指示の重要性

GitHub Copilot に魔法はありません。考える作業を省略できるわけではありません。一見簡単な操作でも、細部を確認すると複雑なことがあります。[Copilot cloud agent に依頼するタスクの範囲][cloud-agent-best-practices]を慎重に設定してください。AI のペアプログラマーとして、段階的に作業し、学び、試し、必要に応じて調整します。生成 AI を利用しても、ソフトウェア開発の基本は変わりません。

## このリポジトリのカスタム指示

前の演習では、カスタム指示と Copilot のガイドに使う方法を学びました。すでにカスタム指示の演習を完了していれば、`.github/copilot-instructions.md` が機能することを確認しています。まだの場合は、cloud agent に作業を割り当てる前に、このリポジトリに用意された指示ファイルを読み取り専用で確認してください。後で影響を確認できます。

GitHub Web UI または起動済みの Codespace で、次のファイルを開きます。

- `.github/copilot-instructions.md` — **Code standards** セクション、特に TypeScript の規約と TSDoc ドキュメントコメントに関する要件を確認します。
- `.github/instructions/unit-tests.instructions.md` — `applyTo` フロントマターで、`**/*.test.ts` ファイルに指示が適用されることを確認します。

次のセクションで `Code lacks documentation` Issue を cloud agent に割り当てると、作成された PR に TSDoc コメント、TypeScript の規約、コメントヘッダーが反映されます。これらの指示ファイルからの影響は、後の演習で PR をレビューするときに確認します。

## Copilot cloud agent の開発環境を設定する

誰が作業する場合でも、コードを作成するには環境の準備とセットアップスクリプトが必要です。ソフトウェアエンジニアのように作業する Copilot にタスクを割り当てる場合も同じです。

Cloud agent は [GitHub Actions][github-actions] を使って作業環境を準備します。`.github/workflows/copilot-setup-steps.yml` に設定する[専用のセットアップワークフロー][setup-workflow]を作成すると、作業開始前に必要な開発ツールと依存関係をインストールできます。演習の流れをわかりやすくするため、あらかじめこのワークフローを設定しています。Node.js、プロジェクトの依存関係、エンドツーエンドテスト用のブラウザーバイナリ、単一 Astro アプリ用にマイグレーションおよびシードされた SQLite データベースを Copilot が利用できます。

```yaml
name: "Copilot Setup Steps"

# リポジトリの「Actions」タブからセットアップ手順をテストできます
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # 必要な最小限の権限を設定します。Copilot の操作には独自のトークンが使われます。
    permissions:
      # セットアップ手順の一部としてリポジトリをクローンする場合 (依存関係のインストールなど) は `contents: read` が必要です。クローンしない場合は、手順の完了後に Copilot が自動でクローンします。
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # フロントエンド / アプリのセットアップ - Node.js (アプリ全体は Astro + Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # ローカル SQLite データベースをマイグレーションし、シードデータを追加します。ビルドとテストでデータを利用できます。
      - name: Set up the database
        run: npm run db:setup
```

一般的な GitHub ワークフローに見えますが、いくつか重要な点があります。

- `copilot-setup-steps` というジョブが 1 つあります。このジョブは Copilot が PR の作業を開始する前に GitHub Actions で実行されます。
- `workflow_dispatch` トリガーが設定されています。リポジトリの **Actions** タブからワークフローを手動実行できます。Copilot が実行するのを待たずに、正常に動作するかテストできます。

## ドキュメントを追加する

ドキュメントの重要性は広く理解されていますが、古い情報が残っていたり、ドキュメントがなかったりするプロジェクトは少なくありません。このような技術的負債は、作業の効率を下げ、コードベースの保守や新しいメンバーの受け入れを難しくします。Copilot はドキュメントの作成を支援できるため、このタスクを cloud agent に依頼できます。後の演習で変更をレビューします。

1. 新しいブラウザータブで github.com のリポジトリを開きます。
2. **Issues** タブを選択します。
3. **New issue** を選択して、新しい Issue のダイアログを開きます。
4. **Blank issue** を選択します。
5. **Title** に `Code lacks documentation` と入力します。
6. **Description** に次の内容を入力します。

    ```plaintext
    Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
    ```

7. **Create** を選択して Issue を作成します。
8. 右側で **Assign to Copilot** を選択し、割り当てダイアログを開きます。

  ![Issue に Copilot を割り当てる](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。
10. **Pull Requests** タブを選択します。
11. 新しく作成された PR を開きます。タイトルは `[WIP]: Code lacks documentation` のようになります。PR が一覧に表示されない場合は、少し待ってからブラウザーを更新します。
12. 数分後、Copilot が To Do リストを作成します。

> [!NOTE]
> Copilot の To Do リストが PR に表示されるまで数分かかることがあります。Copilot は先ほどのワークフローを実行して環境を準備し、プロジェクトを分析して、課題に対する適切なアプローチを決めています。

13. リストと、Copilot が実行するタスクを確認します。
14. PR のタイムラインを下にスクロールし、Copilot が Issue の作業を開始したことを示す更新を確認します。
15. **View session** ボタンを選択します。

  ![Copilot のセッションを表示する](../../../_images/ex4-view-session.png)

> [!CAUTION]
> 表示が更新されない場合は、ウィンドウを再読み込みしてください。

16. ライブセッションをスクロールして、Copilot が課題を解決する様子を確認します。コードを調べて状態を把握し、計画を考えて判断し、コードを作成します。

完了まで数分かかります。Copilot cloud agent の主な利点は、非同期にタスクを実行している間、別の作業を進められることです。この利点を活用するため、cloud agent にもう 1 つのタスクを割り当ててから、アプリケーションに機能を追加する作業を始めます。

## ゲーム詳細ページに関連ゲームのセクションを追加する

GitHub Copilot cloud agent の大きな利点は、作業を分担できることです。デザインチーム向けに関連ゲームを追加する作業が短時間で終わるとしても、その時間をほかの作業に使えます。Copilot cloud agent に依頼しましょう。

1. github.com でリポジトリを開きます。
2. **Issues** タブを選択します。
3. **New issue** を選択して、新しい Issue のダイアログを開きます。
4. 空のテンプレートを使うため、**Blank issue** を選択します。
5. **Title** に `Show related games on the game details page` と入力します。
6. **Description** に次の内容を入力します。

    ```markdown
    We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
    ```

7. **Create** を選択して Issue を作成します。
8. 右側で **Assign to Copilot** を選択し、割り当てダイアログを開きます。

  ![Issue に Copilot を割り当てる](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。

Issue の最初のコメントに 👀 が表示され、Copilot が作業を開始したことがわかります。

![Copilot が Issue の作業中であることを示す目の絵文字](../../../_images/ex4-issue-eyes-emoji.png)

Copilot は 2 つ目の依頼にも取り組んでいます。Copilot cloud agent はソフトウェアエンジニアと同じように非同期で動作するため、作業を常に監視する必要はありません。完了後にレビューできます。続いて、カスタムエージェントの作成と使用を学びます。

## まとめと次のステップ

[GitHub Copilot cloud agent][copilot-agents]について学びました。Issue を Copilot に割り当て、非同期で作業を依頼できます。技術的負債への対応、新機能の作成、別のフレームワークへのコード移行などに利用できます。

この演習では、次の内容を学習しました。

- コード生成環境をカスタマイズする。
- 操作を安全に行う。
- Issue の範囲を明確にする。
- Issue を Copilot に割り当てる。

Copilot がバックグラウンドで作業している間に、カスタムエージェントを作成して使う方法を確認しましょう。[Copilot cloud agent は MCP サーバー][cloud-agent-mcp]も使用できます。また、前のモジュールで確認したカスタム指示も利用します。

## リソース

- [Copilot cloud agent について][copilot-agents]
- [GitHub Issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent のセットアップワークフローに関するベストプラクティス][cloud-agent-best-practices]

| [次のレッスン: カスタムエージェント →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
