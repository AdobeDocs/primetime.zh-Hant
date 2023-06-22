---
description: 您可以從以TVSDK為基礎的傳送器應用程式中轉換任何資料流，並使用瀏覽器TVSDK在Chromecast上播放資料流。
title: 瀏覽器TVSDK的Google Cast應用程式
exl-id: 71077467-8040-4f04-a43b-cc963701c426
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# 瀏覽器TVSDK的Google Cast應用程式{#google-cast-app-for-browser-tvsdk}

您可以從以TVSDK為基礎的傳送器應用程式中轉換任何資料流，並使用瀏覽器TVSDK在Chromecast上播放資料流。

<!--<a id="section_87CE5D6D46F0439EB6E63A742D6DD9C8"></a>-->

啟用鑄造的應用程式有兩個元件：

* 傳送者應用程式，可作為遠端控制項。

   傳送者應用程式包括智慧型手機、個人電腦等。 您可以使用適用於iOS、Android和Chrome的原生SDK來開發應用程式。
* 在Chromecast上執行並播放內容的接收者應用程式。

   >[!IMPORTANT]
   >
   >此應用程式只能是HTML5應用程式。

傳送者與接收者使用Cast SDK傳遞訊息來進行通訊。

## 基本工作流程 {#section_FAF680FF29DA4D24A50AC0A2B6402B58}

以下是此程式的概述：

1. 傳送者應用程式會建立與接收者應用程式的連線。
1. 傳送者應用程式會傳送訊息，以便在接收者應用程式上載入媒體。
1. 接收方應用程式會開始播放。
1. 傳送者應用程式會將播放控制訊息（例如，播放、暫停、搜尋、快速前進、快速倒帶、倒帶、音量變更等）傳送至接收者應用程式。
1. 接收者應用程式會回應這些訊息。

## 訊息格式 {#section_1624159DD51D4C87B3E5803DEEBCB6B7}

您必須定義訊息，讓傳送者與接收者能夠瞭解。 以下是搜尋訊息的範例：

```js
{ 
"type": "seek", 
"seekTo": 10000 
} 
```

透過Cast SDK傳送自訂訊息（例如搜尋訊息）時，需要自訂訊息名稱空間。 以下是JavaScript中的範例：

```js
Custom Message Namespace 
var MSG_NAMESPACE = "urn:x-cast:com.adobe.primetime"; 
```

## 建立連線 {#section_B4D40CABDD3E46FDBE7B5651DFF91653}

>[!IMPORTANT]
>
>建立連線時未涉及瀏覽器TVSDK API。

若要建立連線，傳送者與接收者必須完成下列工作：

* 寄件者必須檢閱平台說明檔案，網址為 [寄件者應用程式開發](https://developers.google.com/cast/docs/sender_apps).
* 接收者會使用Cast接收者API來建立與傳送者應用程式的連線。 例如：

   ```js
   window.castReceiverManager = cast.receiver.CastReceiverManager.getInstance(); 
   
   window.castReceiverManager.onReady = function (event) { /*handle event*/ }; 
   window.castReceiverManager.onSenderConnected = function (event) { /*handle event*/ }; 
   window.castReceiverManager.onSenderDisconnected = function (event) { /*handle event*/ }; 
   
   var customMessageBus = window.castReceiverManager.getCastMessageBus(MSG_NAMESPACE); 
   customMessageBus.onMessage = function (event) { /*handle messages*/ }; 
   
   window.castReceiverManager.start(); 
   ```

## 訊息處理 {#section_3E4814546F5946C9B3E7A1AE384B4FF8}

若要傳送訊息給接收者，請參閱寄件者平台的檔案。

>[!IMPORTANT]
>
>您必須包含自訂訊息名稱空間， `MSG_NAMESPACE` 所有訊息中。

對於接收方應用程式，請遵循轉換接收方API的檔案。

**Chrome型寄件者訊息的範例**

```js
window.session.sendMessage(MSG_NAMESPACE, message, successCallback, errorCallback); //https://developers.google.com/cast/docs/reference/chrome/chrome.cast.Session#sendMessage
```

**Chrome型傳送者事件處理**

將事件處理常式繫結至您的UI元素，以便在觸發對應的事件時傳送訊息。 例如，對於以Chrome為基礎的傳送者應用程式，搜尋事件可能會傳送如下：

```js
document.getElementById("#seekBar").addEventListener("click", seekEventHandler); 
   
function seekEventHandler(event) { 
    seekMessage = { type: "seek", seekTo: player.currentTime }; //player is an instance of AdobePSDK.MediaPlayer 
    window.session.sendMessage(MSG_NAMESPACE, seekMessage, successCallback, errorCallback); 
} 
```

**接收者訊息處理**

在接收者應用程式中，以下是如何處理搜尋訊息的範例：

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
