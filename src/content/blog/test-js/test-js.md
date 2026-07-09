---
title: 'javascriptを試す'
description: 'javascriptの練習をする'
pubDate: '2026-07-03'
heroImage: 'js.png'
tags: ["Astro", "中級者", "日記"]
---

## 文字を震わせてみよう

## 画面を震わせるサンプル（最短コード）

ボタンをクリックすると、画面全体（`body`）が0.2秒間ブルブルと震えるプログラムです。以下のコードを丸ごと `.html` ファイルとして保存すれば、そのままブラウザで動かせます。


## 画面を震わせる（Markdown埋め込み版）

このファイルは、Markdown内に直接HTML、CSS、JavaScriptを記述しています。
対応しているMarkdown閲覧環境（VS Codeのプレビュー、HTML変換ツール、一部のWikiなど）で表示すると、下のボタンを押したときに画面全体が震えます。

---

<!-- 1. アニメーション（CSS）の定義 -->
<style>
  @keyframes screen-shake {
    0% { transform: translate(5px, 5px); }
    20% { transform: translate(-5px, 0px); }
    40% { transform: translate(5px, -5px); }
    60% { transform: translate(-5px, 5px); }
    80% { transform: translate(5px, 0px); }
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


## 画面内に入ると画面が震えるサンプル

ページを下にスクロールしていき、赤いボタンがモニターの表示範囲に入った瞬間に、画面全体（`body`）が自動的にブルブルと震えます。

# 画面内に入ると画面が震えるサンプル（解説コメント付き）

ページを下にスクロールしていき、赤いボタンがモニターの表示範囲に入った瞬間に、画面全体（`body`）が自動的にブルブルと震えます。

<div style="height: 100vh; background: #e0e0e0; display: flex; justify-content: center; align-items: center;">
  <p>↓↓↓ 下にスクロールしてください ↓↓↓</p>
</div>

<style>
  /* 画面を震わせる「動きのレシピ」を定義 */
  @keyframes screen-shake {
    0% { transform: translate(2px, 2px); }      /* 最初：右下に2pxずらす */
    20% { transform: translate(-2px, -1px); }   /* 20%経過：左上にずらす */
    40% { transform: translate(1px, -2px); }    /* 40%経過：右上（やや上）にずらす */
    60% { transform: translate(-1px, 2px); }    /* 60%経過：左下にずらす */
    80% { transform: translate(2px, 1px); }     /* 80%経過：右下にずらす */
    100% { transform: translate(0px, 0px); }    /* 最後：元の位置にキッチリ戻す */
  }

  /* このクラス（スイッチ）が要素についた時だけ、上のアニメーションを実行する */
  .shaking-active {
    /* レシピ名: screen-shake / 変化にかける時間: 0.3秒 / 緩急の付け方: 滑らかに */
    animation: screen-shake 0.3s ease-in-out;
  }

  /* 画面に登場する赤いボタンの見た目を整える */
  .scroll-target-button {
    padding: 20px 40px;
    font-size: 24px;
    font-weight: bold;
    background-color: #ff4444;
    color: white;
    border: none;
    border-radius: 8px;
    margin: 100px auto;
    display: block;
  }
</style>

<button id="scrollDangerButton" class="scroll-target-button">画面に入りました！</button>

<div style="height: 100vh; background: #e0e0e0;"></div>

<script>
  // 他のプログラムと変数名などが衝突しないよう、全体を「即時関数」で包んで保護する
  (function() {
    // 監視したいHTMLのボタン要素を取得
    const btn = document.getElementById('scrollDangerButton');
    // 震わせたい対象（ページ全体のボディ）を取得
    const targetElement = document.body;

    // もしボタンかボディのどちらかが存在しなければ、エラーを防ぐためにここで処理を終了する
    if (!btn || !targetElement) return;

    // 【交差監視API】要素が画面内に入ったかどうかを検知するシステムを作成
    const observer = new IntersectionObserver((entries) => {
      // 監視対象（今回はボタン1つだけですが、仕組み上配列で渡されるためループ処理します）
      entries.forEach(entry => {
        
        // 条件分岐：もしボタンが画面（モニター）の中に「入った」なら
        if (entry.isIntersecting) {
          
          // 1. 連打や再進入対策として、一度震えるクラス（スイッチ）を外す
          targetElement.classList.remove('shaking-active');
          
          // 2. ブラウザに「今すぐ画面の見た目を最新状態にして！」と強制命令する（リフローの発生）
          // これを挟むことで、一度消したクラスを直後に再付与した時、ブラウザが「変化」を正しく認識できます
          void targetElement.offsetWidth; 
          
          // 3. 再び震えるクラスを付与する。これでCSSアニメーションが発動して画面が震える
          targetElement.classList.add('shaking-active');
          
          // 【メモ】もし「1回画面に入って震えたら、それ以降はもう震わせたくない」という場合は、
          // 下の1行のコメントアウト（//）を解除すると、監視をその時点でストップできます。
          // observer.unobserve(entry.target);
        }
      });
    }, {
      // 判定の基準値（しきい値）：0〜1の間で設定
      // 0 = 要素の端っこが「1ピクセルでも」画面に見えた瞬間に合格とする設定
      threshold: 0 
    });

    // 作成した監視システム（observer）に対して、「このボタンを監視してね」とスタートの合図を送る
    observer.observe(btn);
  })();
</script>

---

## 赤・青・黄の箱を3つ作る

JavaScriptで、赤・青・黄の3つの箱をページに追加するサンプルです。

<style>
  .color-boxes {
    display: flex;
    gap: 16px;
    flex-wrap: wrap;
    margin: 20px 0;
  }

  .color-box {
    width: 120px;
    height: 120px;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
  }
</style>