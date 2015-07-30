# Aceとは

ブラウザ上で使えるJavaScript製のテキストエディタです。貧弱なテキストエリアの代替として使うと便利です。特徴として、

* 100言語以上のシンタックスハイライト
* Sublime風、Chrome DevTools風など、自由に選べる多数のテーマ
* マルチカーソル
* リアルタイム構文チェック

などなど、スタンドアロンのエディタと比べても決して引けをとらない高機能なエディタです。

## 公式サイト

http://ace.c9.io/

詳しい使い方を知りたいならばAPI Referenceから。

## サンプルサイト

http://ace.c9.io/build/kitchen-sink.html

各種パラメータの効果を見た目で確認することが出来ます。

# インストール

今回のサンプルでは全てCDNを使用しますので何もインストールする必要はありません。

ダウンロードして使いたい場合は https://github.com/ajaxorg/ace-builds/ ←こちらから。

# 最小のサンプル

```html
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <title>Ace Editor sample</title>
</head>
<body>
  <div id="editor" style="height: 600px"></div>
  <script src="//cdnjs.cloudflare.com/ajax/libs/ace/1.2.0/ace.js"></script>
  <script>
    ace.edit("editor");
  </script>
</body>
</html>
```

## 実行結果

![c1.gif](https://qiita-image-store.s3.amazonaws.com/0/32030/97ecdfd5-8602-b86c-0a56-3c260cabbac4.gif)

## 解説

ace.editメソッドは、引数で指定したIDの要素にAceエディタを埋め込みます。

# 基本的なパラメータのサンプル

```html
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <title>Ace Editor sample</title>
</head>
<body>
  <div id="editor" style="height: 600px"></div>
  <script src="//cdnjs.cloudflare.com/ajax/libs/ace/1.2.0/ace.js"></script>
  <script>
    var editor = ace.edit("editor");
    editor.setTheme("ace/theme/monokai");
    editor.setFontSize(14);
    editor.getSession().setMode("ace/mode/html");
    editor.getSession().setUseWrapMode(true);
    editor.getSession().setTabSize(2);
  </script>
</body>
</html>
```

## 実行結果

![c2.gif](https://qiita-image-store.s3.amazonaws.com/0/32030/f37f8dfc-fda7-d38c-4d5f-a31ea1706f56.gif)

## 解説

ace.editorメソッドは、埋め込まれたテキストエディタ全体を表す[Editor](http://ace.c9.io/#nav=api&api=editor)オブジェクトを返します。

```js
editor.setTheme("ace/theme/monokai");
```

Sublime Textっぽい黒めのテーマを指定します。使えるテーマの一覧は、[Ace Kitchen Sink](http://ace.c9.io/build/kitchen-sink.html)を参照してください。

```js
editor.getSession().setMode("ace/mode/html");
```

getSessionメソッドはひとつの文書と文書モードやカーソルなどを管理する[EditSession](http://ace.c9.io/#nav=api&api=edit_session)オブジェクトを返します。setModeメソッドによってHTMLモードに設定しています。

```js
editor.getSession().setUseWrapMode(true);
```

折り返しありにします。

```js
editor.getSession().setTabSize(2);
```

タブ幅を2にします。

# 自動補完・スニペットのサンプル

```html
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <title>Ace Editor sample</title>
</head>
<body>
  <div id="editor" style="height: 600px"></div>
  <script src="//cdnjs.cloudflare.com/ajax/libs/ace/1.2.0/ace.js"></script>
  <script src="//cdnjs.cloudflare.com/ajax/libs/ace/1.2.0/ext-language_tools.js"></script>
  <script>
    var editor = ace.edit("editor");
    editor.$blockScrolling = Infinity;
    editor.setOptions({
      enableBasicAutocompletion: true,
      enableSnippets: true,
      enableLiveAutocompletion: true
    });
    editor.setTheme("ace/theme/monokai");
    editor.getSession().setMode("ace/mode/javascript");
  </script>
</body>
</html>
```

## 実行結果

![c3.gif](https://qiita-image-store.s3.amazonaws.com/0/32030/197f5abb-7bca-b42b-5920-a328d4675264.gif)

## 解説

```html
<script src="//cdnjs.cloudflare.com/ajax/libs/ace/1.2.0/ext-language_tools.js"></script>
```

自動補完を使う場合は、追加でext-language_tools.jsを読み込む必要があります。

```js
editor.$blockScrolling = Infinity;
```

これはよくわかりませんが、Chromeのコンソールに警告が出るのでその解消策です。

```js
editor.setOptions({
  enableBasicAutocompletion: true,
  enableSnippets: true,
  enableLiveAutocompletion: true
});
```

基本的な自動補完、スニペット、ライブ保管を有効にします。

# Emmetのサンプル

```html
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <title>Ace Editor sample</title>
</head>
<body>
  <div id="editor" style="height: 600px"></div>
  <script src="//cdnjs.cloudflare.com/ajax/libs/ace/1.2.0/ace.js"></script>
  <script src="//cloud9ide.github.io/emmet-core/emmet.js"></script>
  <script src="//cdnjs.cloudflare.com/ajax/libs/ace/1.2.0/ext-emmet.js"></script>
  <script>
    var editor = ace.edit("editor");
    editor.$blockScrolling = Infinity;
    editor.setOptions({
      enableEmmet: true
    });
    editor.setTheme("ace/theme/monokai");
    editor.getSession().setMode("ace/mode/html");
  </script>
</body>
</html>
```

## 実行結果

![c4.gif](https://qiita-image-store.s3.amazonaws.com/0/32030/8a560f13-1e5c-b793-840c-5629ff0ef2b4.gif)

## 解説

素敵な魔法[Emmet](http://docs.emmet.io/)のサンプルです。

```html
<script src="//cloud9ide.github.io/emmet-core/emmet.js"></script>
<script src="//cdnjs.cloudflare.com/ajax/libs/ace/1.2.0/ext-emmet.js"></script>
```

Emmet本体と、AceでEmmetを使うための拡張ファイルを読み込みます。

```js
editor.setOptions({
  enableEmmet: true
});
```

Emmetを有効にします。

# 応用サンプル

```html
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <title>Ace Editor sample</title>
  <link href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>
  <div class="btn-group">
    <div class="btn-group">
      <button class="btn btn-default dropdown-toggle" data-toggle="dropdown"><i class="glyphicon glyphicon-search"></i> <span class="caret"></span></button>
      <ul class="dropdown-menu" id="font-size">
        <li><a href="#" data-size="10">小さい</a></li>
        <li><a href="#" data-size="12">普通</a></li>
        <li><a href="#" data-size="14">大きい</a></li>
      </ul>
    </div>
    <button id="bold" class="btn btn-default"><i class="glyphicon glyphicon-bold"></i></button>
    <button id="save" class="btn btn-default"><i class="glyphicon glyphicon-floppy-save"></i></button>
    <button id="load" class="btn btn-default"><i class="glyphicon glyphicon-folder-open"></i></button>
  </div>

  <div id="editor" style="height: 600px"></div>
  <script src="//code.jquery.com/jquery-2.1.4.min.js"></script>
  <script src="//maxcdn.bootstrapcdn.com/bootstrap/3.3.5/js/bootstrap.min.js"></script>
  <script src="//cdnjs.cloudflare.com/ajax/libs/ace/1.2.0/ace.js"></script>
  <script>
    var editor = ace.edit("editor");
    editor.$blockScrolling = Infinity;
    editor.setTheme("ace/theme/monokai");
    editor.getSession().setMode("ace/mode/html");

    $('#font-size').click(function(e) {
      editor.setFontSize($(e.target).data('size'));
    });
    $('#bold').click(function(e) {
      editor.insert('<strong>' + editor.getCopyText() + '</strong>');
    });
    $('#save').click(function(e) {
      localStorage.text = editor.getValue();
      alert("保存しました。");
    });
    $('#load').click(function(e) {
      if (!confirm("読み込みますか？")) return;
      editor.setValue(localStorage.text, -1);
    });
  </script>
</body>
</html>
```

## 実行結果

![c5.gif](https://qiita-image-store.s3.amazonaws.com/0/32030/50a36d9a-adeb-21cd-886d-7b3f8523a944.gif)

## 解説

Bootstrapによるボタンツールバーを設置し、以下の機能を実装しました。

* エディタのフォントサイズ変更
* 選択範囲をstrongタグで囲って強調
* localStorageに保存
* localStorageからの読み出し

今回はBootstrap部分は解説しません。

```js
editor.insert('<strong>' + editor.getCopyText() + '</strong>');
```

getCopyTextメソッドは選択範囲のテキスト内容を取得します。insertメソッドは現在のカーソル位置にテキストを挿入します。この2つのメソッドを組み合わせて、選択範囲をタグで囲む処理を実現しています。

```js
localStorage.text = editor.getValue();
```

getValueメソッドで現在の文書内容を返し、それをlocalStorageに保存しています。

```js
editor.setValue(localStorage.text, -1);
```

保存された文書の内容を読みだしてsetValueメソッドによりエディタにセットします。第2引数の-1はカーソル位置を文書の先頭にします。
