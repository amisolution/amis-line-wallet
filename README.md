<img align="left" src="https://raw.githubusercontent.com/amisolution/ERC20-AMIS/master/amis-logo3.png" alt="amis-logo3"/>
<img align="right" src="https://raw.githubusercontent.com/amisolution/ERC20-AMIS/master/images/AMIS-QRCODE.png" alt="AMIS-QRCODE" width="100"/>

[![Website Down](https://img.shields.io/badge/website-down-red.svg)](http://erc20-amis.amisolution.net/)&nbsp;
[![Join the Gitchat at https://gitter.im/amis-delta-dex/Lobby](https://badges.gitter.im/amis-delta-dex/Lobby.svg)](https://gitter.im/AMIS-DELTA-DEX/Lobby?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)&nbsp;[![Trade Bounty](https://img.shields.io/badge/trade-bounty-orange.svg)](https://github.com/amisolution/ERC20-AMIS/issues/)&nbsp;[![Twitter AirDrop](https://img.shields.io/badge/Twitter-Airdrop-red.svg)](https://twitter.com/AMIStoken_ERC20)&nbsp;[![Official Twitter](https://img.shields.io/badge/official-twitter-brightgreen.svg)](https://twitter.com/amis_erc20)&nbsp;[![Official AmisForkdelta](https://img.shields.io/badge/official-forkdelta-brightgreen.svg)](https://forkdelta.app/#!/trade/0x949bed886c739f1a3273629b3320db0c5024c719-ETH)
&nbsp;[![Official AmisEtherDelta](https://img.shields.io/badge/official-etherdelta-brightgreen.svg)](https://etherdelta.com/#0x949bed886c739f1a3273629b3320db0c5024c719-ETH)
&nbsp;[![Official BambooRelay](https://img.shields.io/badge/official-bamboorelay-brightgreen.svg)](https://bamboorelay.com/trade/AMIS-WETH)&nbsp;[![Official AmisTokenJar](https://img.shields.io/badge/official-tokenjar-brightgreen.svg)](https://tokenjar.io/amis)
&nbsp;[![ßtesting Dubiex](https://img.shields.io/badge/ßtesting-dubiex-yellow.svg)](https://dubiex.com/AMIS/ETH)&nbsp;[![Official AmisLedgerDex](https://img.shields.io/badge/official-ledgerdex-1330e3.svg)](https://app.ledgerdex.com/#/app/orders/maker-taker/AMIS/0x949bed886c739f1a3273629b3320db0c5024c719/WETH/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2
)&nbsp;[![Official Cryptoderivatives](https://img.shields.io/badge/official-cryptoderivatives-4330e7.svg)](https://cryptoderivatives.market/token/AMIS)&nbsp;[![Official Cryptocompare](https://img.shields.io/badge/official-cryptocompare-brightgreen.svg)](https://www.cryptocompare.com/coins/amis)&nbsp;[![Official DexTracker](https://img.shields.io/badge/official-dextracker-brightgreen.svg)](https://etherscan.io/dextracker?filter=&q=AMIS)
&nbsp;[![ßtesting TokenStore](https://img.shields.io/badge/ßtesting-TokenStore-yellow.svg)](https://token.store/trade/0x949bed886c739f1a3273629b3320db0c5024c719)
&nbsp;[![αtesting EthenMarket](https://img.shields.io/badge/αtesting-ethenmarket-lightgrey.svg)](https://ethen.market/949bed886c739f1a3273629b3320db0c5024c719)&nbsp;[![ßtesting AmisDex](https://img.shields.io/badge/ßtesting-amisdex-lightblue.svg)](https://amisdex.github.io/amis-exchange-www)

What is Amis LineEtherBot?


# Amis LineEtherBot
 Amis LineEtherBot is a simple Mobile Dapp which uses Line Messaging API. Using the Line Messaging API, you can get your AMIS / ETH's balance, issue remittance or transfer money from the Line talk screen. You can also check balance of your Service Provider, issue invoices and make payment with AMIS ERC20 Token and ETH.
 
 * source: https://pragma-curry.com/2018/07/07/221/
 * Works best with Metamask extension: install it metamask.io
 * Check balance : https://impartial-ellipse.glitch.me/accountinfo.html
 * Manage invoice(s) : https://impartial-ellipse.glitch.me/invoice
 * Make transfer : https://impartial-ellipse.glitch.me/transfer
 * Using the Line Messaging API, you can get Ethereum's balance or send money from the Line talk screen.
 
 <img align="left" src="https://camo.qiitausercontent.com/d6ebaf6a8bae3b4555e50340ab233c122a3a86c1/68747470733a2f2f707261676d612d63757272792e636f6d2f77702f77702d636f6e74656e742f75706c6f6164732f323031382f30372f39363038636465383064333161656433623736656632623665363562653965642d312e6a7067" alt="HLD" width="100"/>
 
# usage environment
Ethereum Node - infura.io
Application Server - Glitch
1/ Setting up the Line Messaging API
Register providers and channels with LINE Developers' Start using Messaging API .

For detailed procedures, refer to the last entry Entry Line Messaging API Flex Message .

2/ Acquire the API KEY of infura.io
By registering a mail address from the GET STARTED FOR FREE button of infura.io you can get API KEY.

For detailed procedures, please refer to the last entry ERC 223 token shortly to public on the public chain (for busy people) .

3/ Set the Glitch
Glitch is Paas that Node.js can use. Sign up can also be done with Github's account. 
After logging in, create a new project from New Project.

I created a project named impartial-ellipse for that purpose. 

4/ Install the required modules
Next step consist of adding all necessary modules, the following modules will be added

* linebot - one of LineBotSDK
* web3 - The Javascript API
* nedb - NoSQL unnecessary for installation
In order to add these 3 packages. Click package.json in the Glitch project folder and add it from Add Packages.

5/ Define the class of LineBot
In order to create Reply messages and read / write databases frequently in building LineBot applications, we make the series of processing systems into a class to make it easy to use. (To be exact, it is a pseudo class of ES5.) Reply There are many kinds of messages, but we define only text and buttons that are frequently used. Although it is a little long, it will be easier later if you put it together.

```
const Linebot = function(app) {
   const linebot = require('linebot'); //linebot sdkの読み込み
   const Database = require('nedb'); //nedbの読み込み
   //各ユーザー端末のLineBotの状態を格納するためのデータベースファイルを指定
   const db={};
   db.botstatus = new Database({
      filename: '.database/botstatus', 
      autoload: true
   });
 
  //LineBotのチャンネルID等をコンストラクタに渡しthis.botに代入
   this.bot = linebot({
      channelId: process.env.CHANNEL_ID,
      channelSecret: process.env.CHANNEL_SECRET,
      channelAccessToken: process.env.CHANNEL_ACCESS_TOKEN,
      verify: true
   });
   app.post('/', this.bot.parser());
 
   //Lineからのメッセージやポストバックのイベントを受取り、コールバック関数にイベントを渡す
   this.onMessageEvent = function (callback){
      this.bot.on('message',event => {
            this.setMessageTemplate(event);
            callback(event);
      });
      this.bot.on('postback',event => {
            this.setMessageTemplate(event);
            callback(event);
      });
  }
 
  //ReplyのたびにJSONをいちいち書くのは面倒なので、よく使うテキストやボタンだけ定義。
  //ボタンは４つまで設置できるので、可変長引数にしておく。
  this.setMessageTemplate = function(event){
 
      event.replyText = function(message){
           event.reply([{
              "type": "text",
              "text": message
           }]).then(data => {
                console.log('Success', data);
           }).catch(error => {
                console.log('Failed', error);
           });
      }
 
      event.replyButton = function(/*title,message,button,postback,...*/){
           var obj = {
              "type": "template",
              "altText": arguments[0],
              "template": {
                  "type": "buttons",
                  "thumbnailImageUrl": null,                     
                  "title": arguments[0],
                  "text": arguments[1],
                  "actions": [
                      {
                        "type": "postback",
                        "label": arguments[2],
                        "data": arguments[3],
                      }
                  ]
              }
           }
           for (var i = 0; i < 3; i++) { if(arguments.length > 2*i+4){
                obj.template.actions[i+1]={
                  "type":  "postback",
                  "label": arguments[2*i+4],
                  "data":  arguments[2*i+5] 
                };
             }
           }
          event.reply([obj]).then(data => {
                console.log('Success', data);
           }).catch(error => {
                console.log('Failed', error);
           });
      }
 
      //ユーザー端末のLineBotの状態をデータベースから読み込む
      this.readDatabase = function(lineID){
          return new Promise((resolve, reject) =>  {
              db.botstatus.findOne({ lineid: lineID }, (err, obj) =>{
                   if(err == null && obj!=null){
                       resolve(obj.status);
                   }
                   else if(err == null && obj==null){
                       resolve(null);
                   }
                   else{
                       reject(err);
                   }
              });
          });
      }
 
      //ユーザー端末のLineBotの状態をデータベースに書き込む
      this.writeDatabase = function(lineID,status){
          db.botstatus.findOne({ lineid: lineID }, (err, obj) => {
              if(obj==null){
                  db.botstatus.insert({'lineid':lineID,'status':status});  
              }
              else{
                  db.botstatus.update({ 'lineid': lineID }, { $set: { status: status } }, { multi: true });
              }
          });
      }
}
```
If you prepare the above class
```
const express = require('express');
const app = express();
const bot = new Linebot(app);
bot.onMessageEvent(someFunction);
 
someFunction(event){
   event.replyButton(
      '選んでください','どれが好き？',
      'ビーフカレー','answer=beef',
      'ポークカレー','answer=pork',
      'チキンカレー','answer=chicken'
   );
   event.replyText('テストだよ');
}
```

* Result in:

<img align="left" src="https://camo.qiitausercontent.com/9816761eaa57c2235b3923987bd541bdfe432137/68747470733a2f2f707261676d612d63757272792e636f6d2f77702f77702d636f6e74656e742f75706c6f6164732f323031382f30372f33343135302e6a7067" alt="AmisLine Preview" width="100"/>

6/ Define the class handling Ethereum's web3.js
Since only the balance is acquired, I think that it is sufficient if selection of a chain and validation of an Ethernet address are sufficient.
```
const Ether = function(){
   const Web3 = require('web3');  //web3.jsの読み込み
 
   //mainnet,ropsten,rinkeby,kovanのどれかを指定してnodeとchain idを返す
   //infura.ioで取得したAPIアクセスキーを環境変数に入れて呼び出している。
   this.setChain = function(chain){
        switch(chain){
          case 'mainnet':
             return {'node':'https://mainnet.infura.io/'+ process.env.INFURA_KEY, 'id':1};
             break;
          case 'ropsten':              
             return {'node':'https://ropsten.infura.io/'+ process.env.INFURA_KEY, 'id':3};
             break;
          case 'rinkeby':              
             return {'node':'https://rinkeby.infura.io/'+ process.env.INFURA_KEY, 'id':4};
             break;
          case 'kovan':              
             return {'node':'https://kovan.infura.io/'+ process.env.INFURA_KEY, 'id':42};
             break;
          default:
             return {'node':'https://mainnet.infura.io/'+ process.env.INFURA_KEY, 'id':1};
             break;
       }
   }
 
   //正しいイーサリアムアドレスの形式になっているか確認する
   this.validateAddress = function(address){
      var valid = true;
      if(String(address) == ''){
          valid = false;
      }
      else if(
              String(address).length != 42
          || !String(address).match(/^[0-9a-zA-Z]/)
          || !(String(address).slice(0,2)=='0x')
      ){
          valid = false;
      }
      return valid;
   }
 
   //単位Etherで残高取得する
   this.getBalance = function(chain,address){
      const web3 = new Web3(new Web3.providers.HttpProvider(this.setChain(chain).node));
      return new Promise((resolve, reject) => {
          if(this.validateAddress(address)){
                resolve(web3.fromWei(web3.eth.getBalance(address), "ether").toNumber());
          }
          else{
                reject('Invalid address.');
          }
      });
   }
}
```
7/ Write the main processing
Using the methods created in 5 and 6 above,

1 user sends a LINE message 
2 User state and messages are stored in nedb 
3 Line Messaging API returns Reply (Question) 
4 User sends a LINE message 
Get information from the Ethernet based on the message stored in 5 2 and the message sent in 4. 
6 The state of the user is initialized 
7 Line Messaging API returns Reply (user wants information)

Implement the basic flow of:
```
var Main = function(app){
    const bot = new Linebot(app);
    const ether = new Ether();
 
    //botインスタンスにgetActionメソッドを追加。
    //DBにユーザーの状態が保存されていない場合（初期状態）では、LINEで送られたクエリ形式のアクション
    // (action=showBalance 等)を解析して次のアクションを行う。
 
    bot.getAction = function(event,message){
        try{
            if(typeof(message['action']) == 'undefined' || message['action']==''){
                throw 'No Action Detected.';
            }
            switch(message['action']){
            case 'showBalance':
                bot.writeDatabase(event.source.userId,'action=showbalance&listen=chain');
                event.replyButton(
                    'Select Chain','Select Ethereum chain.',
                    'Mainnet','chain=mainnet',
                    'Ropsten','chain=ropsten',
                    'Rinkeby','chain=rinkeby',
                    'Kovan','chain=kovan'
                );
                break;
            default:
                throw 'No Action Detected.';
                break;
            }
 
          }catch(e){
               event.replyText(e);
          }
    }
 
    //メッセージかポストバックイベントを受け取ったら、まずどちらのイベントか判断する
    this.onMessageEvent = function(event){
        switch(event.type){
           case 'message':
              var message = functions.queryParse(event.message.text);      
              break;
           case 'postback':
              var message = functions.queryParse(event.postback.data);
              break;
           default:
              event.replyText('The event type is not supported.');
              break;
        }
 
        //ユーザーのLINE IDをキーにDBファイルからクエリ形式で状態を取得
        bot.readDatabase(event.source.userId).then(function(statusQuery) {
 
              //クエリ文字列をオブジェクトに変換する関数queryParseを定義しておく
              //action=shobalance等のクエリ形式を解析
              var status = queryParse(statusQuery); 
 
              if(status['action']=='showbalance' && status['listen']=='chain'){
 
                    if(typeof message['chain'] !== 'undefined'){
                        bot.writeDatabase(event.source.userId, 'action=showbalance&listen=address&chain=' + message['chain']); 
                        //chainの選択が終わったら、次はアドレスを取得するよう、ユーザー状態を変化させる。
                        event.replyText('Send '+ message['chain']+ ' Address.');
                    }
                    else{
                        bot.writeDatabase(event.source.userId, null); //ユーザー状態を初期化
                        event.replyText('Failed to select chain.');
                    }
              }
              else if(status['action']=='showbalance' && status['listen']=='address' && typeof status['chain'] !== 'undefined'){
                    ether.getBalance(status['chain'] , event.message.text).then(function(data){
                        event.replyText(data);
                    })
                    .catch(function(err){
                        event.replyText(err);
                    });
                    bot.writeDatabase(event.source.userId, null); //ユーザー状態を初期化
              }
              else{
                  bot.getAction(event,message);  //ユーザー状態を初期化
              }
 
        }).catch(function (err) {
            event.replyText(err);
        });
    }
    bot.onMessageEvent(this.onMessageEvent);
}
const express = require('express');
new Main(express());
```
* When you do the above:
<img align="left" src="https://camo.qiitausercontent.com/ed79ee1483df48d0adb4ef9d4e9f33e29b2e4d16/68747470733a2f2f707261676d612d63757272792e636f6d2f77702f77702d636f6e74656e742f75706c6f6164732f323031382f30372f33343137302e6a7067" alt="AmisLine Preview2" width="100"/>

And I got the Ether balance of Ropsten from the LINE Talk screen.

# Development status

Non production ready.
I have to copy and paste the address. Especially because it assumes operation on a smartphone, it is considerably troublesome.

Main caveat

Since javascript can not be embedded on the LINE talk screen, in the case of remittance etc., it will be a dangerous act of sending a private key to the application server and then signing etc for that purpose we recommend using Metamask.


Line@
https://line.me/R/ti/p/%40crb2330m

# Contributions
Thx [@snst-lab](https://github.com/snst-lab/etherbot)
