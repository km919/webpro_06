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
以下，app5.jsの全文  
const express = require("express");  
const app = express();  

app.set('view engine', 'ejs');  
app.use("/public", express.static(__dirname + "/public"));  

app.get("/hello1", (req, res) => {  
  const message1 = "Hello world";  
  const message2 = "Bon jour";  
  res.render('show', { greet1:message1, greet2:message2});  
});  

app.get("/hello2", (req, res) => {  
  res.render('show', { greet1:"Hello world", greet2:"Bon jour"});  
});  

app.get("/icon", (req, res) => {  
  res.render('icon', { filename:"./public/Apple_logo_black.svg", alt:"Apple Logo"});  
});  

app.get("/luck", (req, res) => {  
  const num = Math.floor( Math.random() * 6 + 1 );    
  let luck = '';  
  if( num==1 ) luck = '大吉';    
  else if( num==2 ) luck = '中吉';  
  console.log( 'あなたの運勢は' + luck + 'です' );  
  res.render( 'luck', {number:num, luck:luck} );  
});  


app.get("/janken", (req, res) => {  
  let hand = req.query.hand;  
  let win = Number(req.query.win) || 0;     
  let total = Number(req.query.total) || 0;   

  console.log({ hand, win, total });  

  const num = Math.floor(Math.random() * 3 + 1);  
  let cpu = '';  
  if (num === 1) cpu = 'グー';  
  else if (num === 2) cpu = 'チョキ';  
  else cpu = 'パー';  

  let judgement = '';  
  if (hand === cpu) { // ユーザーの手とCPUの手が同じ場合は「引き分け」。  
    judgement = '引き分け';  
  } else if ( // ユーザーが勝つ組み合わせの場合は「勝ち」とし、winを1増加する。  
    (hand === 'グー' && cpu === 'チョキ') ||  
    (hand === 'チョキ' && cpu === 'パー') ||  
    (hand === 'パー' && cpu === 'グー')  
  ) {  
    judgement = '勝ち';  
    win += 1;   
  } else { // それ以外は「負け」  
    judgement = '負け';  
  }  

  total += 1; //  ゲームが終了したので、総試行数totalを1増加させる。  

  const display = {  
    your: hand,  
    cpu: cpu,  
    judgement: judgement,  
    win: win,  
    total: total  
  };  
  res.render('janken', display);  
});  

app.get("/chohan", (req, res) => {  
  const choices = ["丁", "半"];  
  
  // ランダムにサーバーの選択を決定  
  const serverChoice = choices[Math.floor(Math.random() * 2)];  
  
  // クエリパラメータからユーザーの選択を取得  
  const userChoice = req.query.choice;  
  
  // 勝敗判定  
  let outcome = '';  
  if (userChoice === serverChoice) {  
    outcome = '勝ち';  
  } else {  
    outcome = '負け';  
  }  

  // `chohan.ejs`にデータを渡してレンダリング  
  res.render('chohan', {  
    userChoice: userChoice,  
    serverChoice: serverChoice,  
    outcome: outcome  
  });  
});  

app.get("/taste", (req, res) => {  
  // ユーザーの選択を取得（クエリパラメータから）  
  const choice = req.query.choice;  

  // 3分の1の確率で「酸っぱい」、3分の2の確率で「甘い」  
  const randomValue = Math.random();  
  const taste = randomValue < 1 / 3 ? "酸っぱい" : "甘い";  

  // 結果をテンプレートに渡す  
  res.render("taste", { choice: choice, taste: taste });  
});

app.listen(8080, () => console.log("Example app listening on port 8080!"));  

  
上記のapp5.jsについて説明する．
app5.jsは7つの機能を持ち，それぞれ hello1，hello2，icon，luck，janken，chohan，taste となっている．
これらの機能を起動する方法はそれぞれ異なるが，一部共通している箇所があるので最初にそれを説明する．  
まずターミナルを開き，app5.jsが入っているディレクトリに移動する．
移動後"node app5.js"と入力し，  
Example app listening on port 8080!  
という表示を確認する．  
次に別のターミナルを開き，"telnet localhost 8080"と入力し，  
Trying ::1...  
Connected to localhost.  
Escape character is '^]'.  
という表示を確認する．  
ここまでが7つの機能全てに共通する箇所である．以下，各機能ごとに起動方法と，機能そのものを説明していく．

hello1  
前述の起動手順を終えた後，  
GET /hello1 HTTP/1.1  
Host: localhost  
と入力し，改行してからエンターキーを押す．



