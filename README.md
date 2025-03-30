# Gemini Search Chat

このアプリケーションは、Google の Gemini API を利用して、ユーザーが入力した質問に対して検索を利用して、回答を生成するシンプルなチャットインターフェースを提供します。

## 主な機能

- Search With Google を利用した検索
- プロジェクト単位での会話管理
- カスタマイズ可能なシステムプロンプト
- 履歴管理
- 全文検索
- 自動マークダウン出力(スレッドごとにファイル出力)
- CSVエクスポート(プロジェクト全体)

## プロジェクト(システムプロンプト)の設定画面

![alt text](<images/スクリーンショット 2025-03-30 21.47.50.png>)

## 使用例

![alt text](<images/スクリーンショット 2025-03-30 21.45.15.png>)



## 機能の詳細

-   **プロジェクト管理:**
    -   プロジェクトの作成、選択
    -   プロジェクトごとのシステムプロンプト設定
    -   プロジェクトの編集（名前、システムプロンプト）
    -   プロジェクトの削除（関連データ含む）
-   **スレッド管理:**
    -   プロジェクト内でのスレッド（チャットセッション）作成
    -   スレッドの選択（最新5件表示、追加読み込み機能付き）
    -   スレッド名の編集
    -   スレッドの削除
-   **チャット機能:**
    -   テキスト入力による Gemini API への質問送信
    -   チャットごとの使用 Gemini モデル選択（Flash / Pro）
    -   マークダウン形式での回答表示（コードブロック対応）
-   **履歴管理と検索:**
    -   SQLite データベースへの会話履歴の自動保存
    -   スレッドごとのマークダウンファイルへのリアルタイム書き出し (`markdown_files` ディレクトリ）
    -   SQLite FTS5 を使用したチャット履歴の全文検索
-   **エクスポート:**
    -   全会話履歴（プロジェクト、スレッド情報含む）の CSV エクスポート

## セットアップ

1.  **リポジトリをクローン:**
    ```bash
    git clone https://github.com/noricha-vr/gemini-search-chat.git # リポジトリURLを確認してください
    cd gemini-search-chat
    ```

2.  **仮想環境の作成と有効化 (推奨):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # Linux/macOS
    # venv\Scripts\activate  # Windows
    ```

3.  **依存関係のインストール:**
    ```bash
    pip install -r requirements.txt
    ```
    *注意: SQLite の FTS5 機能を利用します。必要に応じて適切な SQLite バージョンがインストールされているか確認してください。*

4.  **環境変数の設定:**
    `.env.example` をコピーして `.env` ファイルを作成し、お使いの Gemini API Key を設定します。
    ```bash
    cp .env.example .env
    # nano .env またはお好みのエディタで API キーを設定
    # 例: GEMINI_API_KEY="YOUR_API_KEY_HERE"
    # 例: MARKDOWN_SAVE_DIR="path/to/your/markdown_directory" # (オプション) マークダウンの保存先。デフォルトは "markdown_files"
    ```
    - `GEMINI_API_KEY`: Google AI Studio で取得した API キーを設定します。
    - `MARKDOWN_SAVE_DIR` (オプション): スレッドごとのマークダウンファイルが保存されるディレクトリを指定します。指定しない場合は、プロジェクトルートに `markdown_files` ディレクトリが作成されます。

5.  **アプリケーションの実行:**
    ```bash
    streamlit run app.py
    ```
    ブラウザで [http://localhost:8501](http://localhost:8501) にアクセスします。

## 使い方

1.  サイドバーで **プロジェクトを選択** するか、**「新しいプロジェクトを作成」** します。
2.  **「新しいスレッドを開始」** するか、既存のスレッドを選択します。
3.  メインエリアで使用する **Gemini モデルを選択** します。
4.  下部のチャット入力ボックスにメッセージを入力して送信します。
5.  サイドバーでプロジェクトの **編集** や **削除**、スレッドの **編集** や **削除** が可能です。
6.  サイドバーの **検索** 機能で過去のメッセージを検索できます。
7.  サイドバーの **エクスポート** 機能で全データを CSV としてダウンロードできます。

## 今後の開発予定 (Ideas)

-  Docker 対応
- 全文検索時のUI改善
- スレッド名を設定
