# 建立第一個程式 🐦- windows

## 👉 建立一個資料夾📁 \(自行命名\)

![](.gitbook/assets/image%20%2822%29.png)

## 👉 建立一個`package.json`的純文字檔案📄，並輸入內容如下\(name 請根據你建的檔案輸入\)

![](.gitbook/assets/image%20%2823%29.png)

```javascript
{
  "name": "你的資料夾名稱",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "node ."
  },
  "author": "",
  "license": "ISC"
}
```

## 👉 開啟【Node.js command prompt】，並輸入自己的資料夾路徑

![](.gitbook/assets/image%20%2831%29.png)

## 👉 為了讓Node.js和Line溝通，要安裝 linebot 和 express 這二個模組，指令如下

```javascript
npm install linebot express --save
```

![](.gitbook/assets/image%20%282%29.png)

![&#x5B8C;&#x6210;&#x5F8C;&#xFF0C;&#x5167;&#x5BB9;&#x5927;&#x81F4;&#x5982;&#x6B64;&#x5716;&#x96F7;&#x540C;](.gitbook/assets/image%20%286%29.png)

## 👉 在資料夾中建立一個`index.js`檔案📄，內容如下

```javascript
// line套件設定
var linebot = require('linebot');
var express = require('express');

// line 帳號設定
var bot = linebot({
  channelId: '你自己Line的channelId',
  channelSecret: '你自己Line的channelSecret',
  channelAccessToken: '你自己Line的channelAccessToken'
});

// 聊天機器人回話設定
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

// webhook 設定
const app = express();
const linebotParser = bot.parser();
app.post('/', linebotParser);

// port 設定
var server = app.listen(process.env.PORT || 8080, function() {
  var port = server.address().port;
  console.log('目前的port是', port);
});
```

## 👉 在資料夾中建立一個`.gitignore`檔案📄，內容如下

```javascript
node_modules
```

## 👉 打開 cmd，跟剛剛一樣先導到自己的資料夾

![](.gitbook/assets/image%20%2852%29.png)

## 👉 登入 heroku

![](.gitbook/assets/image%20%2845%29.png)

## 👉 輸入資訊

![](.gitbook/assets/image%20%2851%29.png)

## 👉 初始化

📣 資料夾名稱要寫對，否則會有 error

![](.gitbook/assets/image%20%2850%29.png)

## 👉 新增檔案，並且給予註解

![](.gitbook/assets/image%20%2846%29.png)

## 👉 上傳

![](.gitbook/assets/image%20%2848%29.png)

## 👉 回到 heroku 【Settings】中的【Domains】 複製右側網址

![](.gitbook/assets/image%20%2847%29.png)

## 👉 複製到 line 的【Webhook settings】中，完成後按下【Update】，再按下【Verify】

![](.gitbook/assets/image%20%2853%29.png)

![](.gitbook/assets/image%20%2849%29.png)

## 👉 測試

![](.gitbook/assets/image%20%2839%29.png)

