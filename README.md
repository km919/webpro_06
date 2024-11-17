# webpro_06
2024 10/29


# webpro_06
2024 11/05

```javascript
console.log( 'Hello' );
```

```javascript
console.log('aaaaa');
```

```mermaid
flowchart TD;
開始 --> 終了;
```

```mermaid
flowchart TD;
start["開始"];
end1["終了"]
if{"条件に合うか"}
win["勝ち"]
loose["負け"]
start --> if
if -->|yes| win
win --> end1
if -->|no| loose
```

ファイル名 | 説明 
-|-
app5.js | プログラム本体 
public/janken.html | じゃんけんの開始画面 
janken.ejs | じゃんけん開始の画面で表示される文字
## このプログラムについて
## ファイル一覧

## app5.js 全体のドキュメント（レポート課題）

app.get("/hello1", (req, res) => {

  const message1 = "Hello world";

  const message2 = "Bon jour";

  res.render('show', { greet1:message1, greet2:message2});
  
});

この




```mermaid
app.get("/hello2", (req, res) => {
  res.render('show', { greet1:"Hello world", greet2:"Bon jour"});
});
```




```mermaid
app.get("/icon", (req, res) => {
  res.render('icon', { filename:"./public/Apple_logo_black.svg", alt:"Apple Logo"});
});
```