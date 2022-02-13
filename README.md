#### 開発メモ
ワークフロー
<br><img width="600" src="https://user-images.githubusercontent.com/40127279/127758761-7c94eb45-9f6a-4b46-b184-761e03dab45a.png">

### 1.URLを調べてみる
　[植物Q&Aのトップ](https://jspp.org/hiroba/q_and_a/)
<br>　Q&Aの一覧が表示されています。回答日が最新の順番になっているようです
<br>　3226件という総数、一覧の明細が20行、ページしたのインジケーターの最大が162ページ
<br>　わかり易いですね
<br>　一覧の明細には4桁のIDがありますが、こちらは登録日順で、歯抜けもあるようです
<br>　
<br>　個々のQ&AのURLは　https://jspp.org/hiroba/q_and_a/detail.html?id=xxxx 
<br>　IDがわかれば簡単にURLを生成できますね
<br>　
<br>　ワークフローを考えましょう
<br>　HOTKEYスタートで選択中のテキストがある場合はそのテキストでQ&Aを検索
<br>　選択中のテキストがない場合は、トップページから最大ページを取得して、
<br>　ランダムな1ページを選んで、そのページの目次をAlfredに表示させるという感じ
### 2.選択テキストの有無で分岐する
　HOTKEYでselection in macOSを取得して、conditionalユーティリティを使って{query}の
<br>　有無を判定します
<br>　選択テキストがない場合は、20行のQ&AをリターンさせるためScriptFiltetに処理を渡します
<br>　選択テキストがある場合は、RunScriptでURLを組み立てています
<br>　（OpenURLでもできますが、今回はOpenURLをひとつにしています）
<br>　
<br>　RunScript
<br>　<img width="600" src="https://user-images.githubusercontent.com/40127279/127758823-02fd90f2-3d2f-4a11-8f1c-a9fa5071fa43.png">
### 3.JSONフォーマットを作成する
　ScriptFilterの中身となる部分ですが、他のRSS系のLesson同様の作りで
<br>　cURLでソースを取得、grepやsedで必要部分の抽出、Jsonの作成の流れです
<br>　今回は最初に目次ページの最大数を取得するのでURLアクセスが1回多くなっています　
<br>　ソースにコメントがあるので参考にしてください
<br>　
<br>　ScriptFilter
<br>　<img width="600" src="https://user-images.githubusercontent.com/40127279/127758831-5c0c2728-26c8-4828-93a9-9c27efccfd90.png">
### 4.フローを統合する
　最後のOpen URLは分岐した2つのフローを同時に受けています 
<br>　こんなフローも描けるということで実装してみました
<br>　このためOpenURLで実際にアクセスするURLは{query}として、事前に組み立てています
<br>
#### 背景
　以前から、alfredのfeaturesのカスタムサーチとして、下記のURLでの検索を登録して
<br>　いました
<br>　https://jspp.org/hiroba/q_and_a/?key={query}&target=full
<br>　今回ランダムサーチも付け加えてワークフロー化してみした
#### 取扱説明
### 機能:
　日本植物生理学会のHP『みんなのひろば』の植物Q&Aを検索もしくはランダム表示する
### インストール:
　1.[Alfredworkflow](https://github.com/KitanoTamotsu/plant/releases/download/1.0/plant.alfredworkflow.zip)をダウンロード 
<br>　2.ファイルをダブルクリックしてワークフローに登録
### 使い方:
　・文字列を選択してHotkey『⌃p』を入力（Hotkeyはご自身での設定が必要です）
<br>　・表示されたAlfredバーに数字を入力
<br>
<br>
[トップページに戻る](https://kitanotamotsu.github.io/)

