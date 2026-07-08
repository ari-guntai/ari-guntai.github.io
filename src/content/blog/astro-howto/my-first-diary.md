---
title: '初めてのマイ日記'
description: '自分で新しく作った初めてのテスト記事です。'
pubDate: '2026-07-03'
heroImage: 'img/caree.png'
tags: ["Astro", "中級者", "日記"]
---

ここには普通の文章を書きます。今日はAstroの勉強をしています！

# 重要※mdは記号の後に半角スペースが必要
文章の前に#を付けるとh1と同じ意味になる。
### #の数を増やすとh6に近づいて文字が小さくなる


- ついに自分のPCでブログが動いた！
- Markdownの書き方をマスターした
- エラーが出ても怖くなくなった

文字の前に(-)を入れると箇条書きリストになる  
文字の前に-を付けるとhtmlでいう\<ul>の\<li>の書き方

## これからやりたいこと
1. ブログのデザインを可愛くする
2. スマホで撮影した**画像**を表示させてみる
3. 友達に自慢する（笑）

文字の前に(数字.)を入れると数字付きリストになる  
htmlでいう\<ol>の\<li>の書き方

## 改行
マークダウンで改行するには
- 文章の最後に半角スペースを２つ入れることで文章が改行される
- 文章の最後に\<br>を入れる<br>
- 文章と文章の間に改行を入れる

## テーブルの挿入
| KANI   | UNI      | サーモン |
| ------ | -------- | -------- |
| イクラ | マグロ   | たまご   |
| カニ   | ラーメン | からあげ |


## テキストのカラー設定<br>

- マークダウンでは色を変える方法がない
- そのためHTMLの記載方法を使い<span style="color: cyan; ">色を変更</span>する
- \<span style="color: cyan; ">文章\</span><br>

## 画像

![ロコモコ](img/caree.png)
\![画像説明]\(img/caree.png(画像ファイルの場所))

## javascript

javascriptのデモ<br>
mdファイルの中にhtmlの形式で\<style>や\<script>を書くと認識してくれる

<div class="counter-container">
  <button id="my-counter-btn" class="custom-btn">
    クリックしてね
  </button>
  <p class="counter-text">
    ボタンを押した回数: <span id="my-count-display">0</span> 回
  </p>
</div>

<style>
  .counter-container {
    margin: 20px 0;
    padding: 15px;
    border: 1px solid #e2e8f0;
    border-radius: 8px;
    background-color: #f8fafc;
    display: inline-block;
  }
  .custom-btn {
    padding: 8px 16px;
    background-color: #3b82f6;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-weight: bold;
    transition: background-color 0.2s;
  }
  .custom-btn:hover {
    background-color: #2563eb;
  }
  .counter-text {
    margin-top: 10px;
    font-size: 1.1rem;
    color: #334155;
  }
  #my-count-display {
    font-weight: bold;
    color: #ef4444;
    font-size: 1.3rem;
  }
</style>

<script>
  // 何回押されたかを記録する変数
  let count = 0;

  // HTMLの要素（ボタンと文字を表示する場所）をJavaScriptで取得
  const button = document.getElementById('my-counter-btn');
  const display = document.getElementById('my-count-display');

  // ボタンがクリックされたときの処理を設定
  if (button && display) {
    button.addEventListener('click', () => {
      count++; // カウントを1増やす
      display.textContent = count.toString(); // 画面の数字を書き換える
    });
  }
</script>
