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
```













