---
description: 您可以從以TVSDK為基礎的傳送者應用程式轉換任何串流，並使用瀏覽器TVSDK在Chromecast上播放串流。
title: 適用於瀏覽器TVSDK的Google Cast應用程式
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---


# 瀏覽器TVSDK適用的Google Cast應用程式{#google-cast-app-for-browser-tvsdk}

您可以從以TVSDK為基礎的傳送者應用程式轉換任何串流，並使用瀏覽器TVSDK在Chromecast上播放串流。

<!--<a id="section_87CE5D6D46F0439EB6E63A742D6DD9C8"></a>-->

啟用Cast的應用程式有兩個元件：

* 傳送者應用程式，可當成遙控器。

   傳送者應用程式包括智慧型手機、個人電腦等。 此應用程式可使用iOS、Android和Chrome適用的原生SDK來開發。
* 接收器應用程式，可在Chromecast上執行並播放內容。

   >[!IMPORTANT]
   >
   >此應用程式只能是HTML5應用程式。

傳送者和接收者使用Cast SDK來傳送訊息。

## 基本工作流{#section_FAF680FF29DA4D24A50AC0A2B6402B58}

以下是此程式的概述：

1. 傳送者應用程式會建立與接收者應用程式的連線。
1. 傳送者應用程式會傳送訊息，將媒體載入接收者應用程式。
1. 接收器應用程式會開始播放。
1. 傳送者應用程式會將播放控制訊息（例如播放、暫停、搜尋、快進、快倒轉、倒轉、音量變更等）傳送至接收者應用程式。
1. 接收器應用程式會對這些訊息做出反應。

## 消息格式{#section_1624159DD51D4C87B3E5803DEEBCB6B7}

您必須定義訊息，讓傳送者和接收者瞭解。 以下是尋道訊息的範例：

```js
{ 
"type": "seek", 
"seekTo": 10000 
} 
```

當透過Cast SDK傳送自訂訊息（例如搜尋訊息）時，需要自訂訊息命名空間。 以下是JavaScript中的範例：

```js
Custom Message Namespace 
var MSG_NAMESPACE = "urn:x-cast:com.adobe.primetime"; 
```

## 建立連接{#section_B4D40CABDD3E46FDBE7B5651DFF91653}

>[!IMPORTANT]
>
>建立連線時不涉及瀏覽器TVSDK API。

要建立連接，發送方和接收方必須完成以下任務：

* 傳送者必須檢閱位於[傳送者應用程式開發](https://developers.google.com/cast/docs/sender_apps)的平台檔案。
* 接收器使用Cast接收器API來建立與傳送者應用程式的連線。 例如：

   ```js
   window.castReceiverManager = cast.receiver.CastReceiverManager.getInstance(); 
   
   window.castReceiverManager.onReady = function (event) { /*handle event*/ }; 
   window.castReceiverManager.onSenderConnected = function (event) { /*handle event*/ }; 
   window.castReceiverManager.onSenderDisconnected = function (event) { /*handle event*/ }; 
   
   var customMessageBus = window.castReceiverManager.getCastMessageBus(MSG_NAMESPACE); 
   customMessageBus.onMessage = function (event) { /*handle messages*/ }; 
   
   window.castReceiverManager.start(); 
   ```

## 消息處理{#section_3E4814546F5946C9B3E7A1AE384B4FF8}

要向接收方發送消息，請參閱發送方平台的文檔。

>[!IMPORTANT]
>
>您必須在所有消息中包含自定義消息namespace `MSG_NAMESPACE`。

若是接收器應用程式，請依照轉播接收器API的檔案進行。

**Chrome型傳送者訊息範例**

```js
window.session.sendMessage(MSG_NAMESPACE, message, successCallback, errorCallback); //https://developers.google.com/cast/docs/reference/chrome/chrome.cast.Session#sendMessage
```

**以Chrome為基礎的傳送者事件處理**

將事件處理常式系結至UI元素，當觸發對應事件時，這些元素會傳送訊息。 例如，對於以Chrome為基礎的傳送者應用程式，搜尋事件可能會傳送如下：

```js
document.getElementById("#seekBar").addEventListener("click", seekEventHandler); 
   
function seekEventHandler(event) { 
    seekMessage = { type: "seek", seekTo: player.currentTime }; //player is an instance of AdobePSDK.MediaPlayer 
    window.session.sendMessage(MSG_NAMESPACE, seekMessage, successCallback, errorCallback); 
} 
```

**接收者訊息處理**

從接收器應用程式中，以下是如何處理搜尋訊息的範例：

```js
customMessageBus.onMessage = function (event) { 
    var message = JSON.parse(event.data); 
    switch (message.type) { 
        case "seek":  
            player.seek(parseInt(message.seekTo)); 
            break; 
        //code for handling other events 
        default:  
            break; 
    } 
}; 
```

