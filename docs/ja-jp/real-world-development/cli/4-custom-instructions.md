---
title: "レッスン 4 - カスタム指示で Copilot をガイドする"
description: "リポジトリの指示を確認し、ドキュメント標準を追加して、フィルター機能のコードに適用します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

生成 AI を使ううえで、コンテキストは重要です。タスクを特定の方法で実行する必要がある場合は、Copilot がそのガイダンスを参照できるようにします。[指示ファイル][instruction-files]には、求めるコードの内容だけでなく、その構成方法も記載します。フィルター機能を実装したので、Copilot が使った指示を確認し、ドキュメント標準を追加してコードに適用します。

このレッスンでは、次の内容を学習します。

- リポジトリの指示とパス単位の指示ファイルがエージェントに適用される方法
- コーディング標準が守られるように指示ファイルを更新する方法
- 指示ファイルがコードに与える影響

## シナリオ

Tailspin Toys には、開発手法に関するガイドラインと要件があります。たとえば、次のようなものです。

- コメントでは、コードを言い換えるのではなく、目的や自明でない判断を説明します。
- `db/` と `src/lib/` のエクスポートされた関数には、目的、パラメーター、戻り値を説明する TSDoc/JSDoc を記載します。`db` を引数として受け取る場合は、その引数も説明します。
- 再利用可能な Astro コンポーネントには `Props` の契約を記載し、関連コードが変更されたときにコメントも最新の状態に保ちます。
- 既存の書式設定と lint のガイダンスに従います。

指示ファイルを使うと、これらの開発手法に沿ってタスクを実行するために必要な情報を Copilot に伝えられます。

## 指示ファイル

カスタム指示では、Copilot がコーディングスタイルや要件を理解できるように、コンテキストと設定を提供します。優先するコーディング規約やライブラリ、コードコメントの形式などを指定することで、より適切な提案やコードスニペットを得られます。リポジトリ全体に適用する指示も、特定の種類のファイルやタスクに適用する指示も作成できます。

指示ファイルには次の 2 種類があります。

- `.github/copilot-instructions.md` は、リポジトリに関するすべてのリクエストで Copilot に送信される単一の指示ファイルです。多くのリクエストに関係するプロジェクトレベルの情報を記載します。
- `.github/instructions/*.instructions.md` は、特定の言語、ファイル種別、タスクに関するガイドラインを記載します。

> [!NOTE]
> ほかの形式の指示とそのサポート状況は、環境によって異なります。特定の形式に依存する前に、[カスタム指示のサポートに関するリファレンス][custom-instructions-support]を確認してください。

## このプロジェクトのカスタム指示ファイルを確認する

開始しやすいよう、スタータープロジェクトには指示ファイルが用意されています。変更を加える前に、既存ファイルを確認して効果を把握しましょう。

1. Codespace に戻ります。
2. Codespaces のエディターで (ターミナルではなく) `.github/copilot-instructions.md` を開きます。
3. プロジェクトの簡単な説明とコーディングガイダンスを確認します。これらの指示は、このリポジトリで Copilot を使うすべての操作に適用されます。
4. `.github/instructions` フォルダーを開いて内容を確認します。Astro ファイル、Drizzle データレイヤー、テストなどに関する指示があります。
5. `.github/instructions/unit-tests.instructions.md` を開き、先頭の `applyTo` フィールドを確認します。ここでは、指示の適用先となるファイルを決める glob を指定します。
6. `.github/instructions/drizzle.instructions.md` を開き、ほかの指示ファイルやプロジェクト内の既存ファイルへのリンクを確認します。大きな指示を再利用できる小さなファイルに分け、コード生成で参考にするファイルを示せます。

## チームのガイダンスに合わせて指示ファイルを更新する

用意されたファイルは出発点として十分ですが、まだ不足があります。メインの `copilot-instructions.md` を変更し、新しく生成される TypeScript に TSDoc コメントを追加する標準を設定します。

1. `.github/copilot-instructions.md` で、**Code formatting guidance** というセクションを探します。35 行目付近にあります。
2. 最後の箇条書きに次の行を追加します。

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

ファイルは自動的に保存されます。

## 更新したガイダンスを使う

Copilot CLI は、会話の開始時にリポジトリの指示を読み込みます。指示を保存したら、フィルター機能の会話を終了して再開します。機能のコンテキストを保ったまま、新しい指示を読み込めます。

1. フィルター機能の会話を開いている場合は、`/exit` を入力して閉じます。Copilot CLI は会話を自動的に保存します。
2. リポジトリルートで `game-filters-cli` ブランチをチェックアウトし、保存済みの会話を再開します。

   ```bash
   copilot --resume
   ```

   選択を求められたら、フィルター機能の会話を選び、`game-filters-cli` ブランチがチェックアウトされていることを確認します。
3. 次のプロンプトで更新したガイダンスを適用するよう Copilot に依頼します。

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. `/diff` を入力し、変更された TypeScript ファイルを確認します。新しい TSDoc コメントが追加され、コードを正確に説明していることを確認します。

## まとめと次のステップ

Copilot CLI が指示ファイルからコンテキストを得る方法を確認し、新しい標準を機能に適用しました。このレッスンでは、次の内容を学習しました。

- リポジトリの指示とパス単位の指示ファイルがエージェントに適用される方法
- コーディング標準が守られるように指示ファイルを更新する方法
- 指示ファイルがコードに与える影響

次は、再利用可能な `quality-checks` スキルを[カスタマイズして実行し][next-lesson]、lint とテストが一貫して実行されるようにします。

## リソース

- [Copilot CLI にカスタム指示を追加する][instruction-files]
- [カスタム指示のサポート][custom-instructions-support]
- [カスタム指示を作成するためのベストプラクティス][instructions-best-practices]
- [Awesome Copilot — 指示ファイルなどのリソース集][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
