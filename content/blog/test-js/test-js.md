---
title: 'javascriptを試す'
description: 'javascriptの練習をする'
pubDate: '2026-07-03'
heroImage: 'js.png'
tags: ["Astro", "中級者", "日記"]
---

## 文字を震わせてみよう

# 画面を震わせるサンプル（最短コード）

ボタンをクリックすると、画面全体（`body`）が0.2秒間ブルブルと震えるプログラムです。以下のコードを丸ごと `.html` ファイルとして保存すれば、そのままブラウザで動かせます。


# 画面を震わせる（Markdown埋め込み版）

このファイルは、Markdown内に直接HTML、CSS、JavaScriptを記述しています。
対応しているMarkdown閲覧環境（VS Codeのプレビュー、HTML変換ツール、一部のWikiなど）で表示すると、下のボタンを押したときに画面全体が震えます。

---

<!-- 1. アニメーション（CSS）の定義 -->
<style>
  @keyframes screen-shake {
    0% { transform: translate(2px, 2px); }
    20% { transform: translate(-2px, 0px); }
    40% { transform: translate(2px, -2px); }
    60% { transform: translate(-2px, 2px); }
    80% { transform: translate(2px, 0px); }
    100% { transform: translate(0px, 0px); }
  }

  .shaking-active {
    animation: screen-shake 1s linear;
  }

  /* ボタンのデザイン */
  .shake-trigger-button {
    padding: 12px 24px;
    font-size: 18px;
    font-weight: bold;
    cursor: pointer;
    background-color: #ff4444;
    color: white;
    border: none;
    border-radius: 6px;
    margin: 20px 0;
    box-shadow: 0 4px 6px rgba(0,0,0,0.1);
  }
  .shake-trigger-button:active {
    transform: scale(0.98);
  }
</style>

<!-- 2. ボタン要素（HTML） -->
<button id="mdDangerButton" class="shake-trigger-button">画面を震わせる</button>

<!-- 3. 動作を制御するスクリプト（JavaScript） -->
<script>
  // 他のスクリプトと衝突しないように即時関数で包む
  (function() {
    const btn = document.getElementById('mdDangerButton');
    // 画面全体（body）をターゲットにする
    const targetElement = document.body;

    if (btn && targetElement) {
      btn.addEventListener('click', () => {
        // 連打対応：一度クラスを外す
        targetElement.classList.remove('shaking-active');
        // リフロー（再描画）を発生させる
        void targetElement.offsetWidth;
        // クラスを追加して震えさせる
        targetElement.classList.add('shaking-active');
      });
    }
  })();
</script>

---

### ⚠️ 注意点
Markdownの仕様上、**GitHubやQiita、NotionなどのWebサービス上では、セキュリティ（XSS対策）のためJavaScript（`<script>`タグ）の実行が自動的に禁止（サニタイズ）されます。**

このコードが実際に作動するのは、以下のような環境です：
1. **VS Code** のMarkdownプレビュー機能（スクリプトの実行を許可する設定にしている場合）
2. MarkdownをHTMLに変換して公開する独自のビルド環境（マニアックなブログなど）
3. HTMLの直接記述・実行を許可しているMarkdownローカルエディタ
