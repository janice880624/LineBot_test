# 用 LineBot 點燈

#### 👉 打開`index.js`檔案📄

```javascript
var linebot = require('linebot');
var express = require('express');

var bot = linebot({
  channelId: '你自己Line的channelId',
  channelSecret: '你自己Line的channelSecret',
  channelAccessToken: '你自己Line的channelAccessToken'
});

bot.on('message', function(event) {
  if (event.message.type = 'text') {
    var msg = event.message.text;
    event.reply(msg).then(function(data) {
      console.log(msg);
    }).catch(function(error) {
      console.log('錯誤產生，錯誤碼：'+error);
    });
  }
});

const app = express();
const linebotParser = bot.parser();
app.post('/', linebotParser);

var server = app.listen(process.env.PORT || 8080, function() {
  var port = server.address().port;
  console.log('目前的port是', port);
});
```

#### 👉 設定開發版

![](.gitbook/assets/jie-tu-20210109-xia-wu-3.09.09.png)

```javascript
// 開發版設定
var myBoardVars = { board: 'Smart', device: '你的 Device ID', transport: 'mqtt' };

boardReady(myBoardVars, true, function (board) {
   myBoard = board;
   board.systemReset();
   board.samplingInterval = 50;
});
```

#### 👉 定義元件

![](.gitbook/assets/jie-tu-20210109-xia-wu-3.12.40.png)

```javascript
var rgbled;

// 在剛剛的程式中加入三色led的腳位設定
boardReady(myBoardVars, true, function (board) {
   myBoard = board;
   board.systemReset();
   board.samplingInterval = 50;
   rgbled = getRGBLedCathode(board, 15, 12, 13); 
});
```

#### 👉 修改原本機器人收訊息的程式 （修改中）

```javascript
bot.on('message', function (event) {
   var myReply = '';
   if (event.message.type === 'text') {
      myReply = processText(event.message.text);
   }
   if (event.message.type === 'sticker') {
      myReply = '你太幽默了！';
      console.log('sticker');
   }
   if (event.message.type === 'image') {
      myReply = '這照片好帥！';
   }

   event.reply(myReply).then(function (data) {
      // success 
      console.log(myReply);
   }).catch(function (error) {
      // error 
      console.log('error');
   });
});
```

#### 👉 再加一點智慧功能，幫你判斷是否斷線

```javascript
function deviceIsConnected() {
   if (myBoard === undefined) {
      return false;
   }
   else if (myBoard.isConnected === undefined) {
      return false;
   }
   else {
      return myBoard.isConnected;
   }
}
```

#### 👉 最重要也是最難的一部分

```javascript
function processText(myMsg) {
   var myResult = '';

   if (myMsg === '你好' || myMsg === '早安' || myMsg === '午安' || myMsg === '晚安')
      myResult = myMsg;

   else if (myMsg === '開燈') {
      if (!deviceIsConnected())
         myResult = '裝置未連接！';
      else {
         rgbled.setColor('#ff0000');
         myResult = '開燈';
      }
   }

   else if (myMsg === '關燈') {
      if (!deviceIsConnected())
         myResult = '裝置未連接！';
      else {
         rgbled.setColor('#000000');
         myResult = '關燈';
      }
   }

   else {
      myResult = '我聽不懂QQ 哈哈';
   }

   return myResult;
}
```

#### 👉 上傳三步驟

1. `git add .`
2. `git commit -am "註解"`
3. `git push heroku master`

![](.gitbook/assets/jie-tu-20210109-xia-wu-2.58.37.png)

