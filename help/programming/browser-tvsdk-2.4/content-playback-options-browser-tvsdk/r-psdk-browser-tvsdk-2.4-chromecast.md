---
description: 您可以從基於TVSDK的發送程式應用中播放任何流，並使用瀏覽器TVSDK在Chromecast上回放流。
title: Google瀏覽器TVSDK播放應用
exl-id: 71077467-8040-4f04-a43b-cc963701c426
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Google瀏覽器TVSDK播放應用{#google-cast-app-for-browser-tvsdk}

您可以從基於TVSDK的發送程式應用中播放任何流，並使用瀏覽器TVSDK在Chromecast上回放流。

<!--<a id="section_87CE5D6D46F0439EB6E63A742D6DD9C8"></a>-->

啟用Cast的應用有兩個元件：

* 發送程式應用，充當遙控器。

   發件人應用包括智慧手機、個人電腦等。 該應用可以使用iOS、安卓和Chrome的本機軟體開發工具包來開發。
* 接收程式在Chromecast上運行，播放內容。

   >[!IMPORTANT]
   >
   >此應用只能是HTML5應用。

發送方和接收方通過使用Cast SDK傳遞消息進行通信。

## 基本工作流 {#section_FAF680FF29DA4D24A50AC0A2B6402B58}

以下是該過程的概述：

1. 發送方應用與接收方應用建立連接。
1. 發送方應用發送消息以在接收方應用上載入媒體。
1. 接收器應用開始播放。
1. 發送方應用將播放控制消息（如播放、暫停、查找、快進、快倒、倒帶、音量更改等）發送給接收方應用。
1. 接收器應用會對這些消息做出反應。

## 消息格式 {#section_1624159DD51D4C87B3E5803DEEBCB6B7}

您必須定義郵件，以便發件人和收件人能夠理解。 下面是查找消息的示例：

```js
{ 
"type": "seek", 
"seekTo": 10000 
} 
```

通過Cast SDK發送自定義消息（如查找消息）時，需要自定義消息命名空間。 以下是JavaScript中的示例：

```js
Custom Message Namespace 
var MSG_NAMESPACE = "urn:x-cast:com.adobe.primetime"; 
```

## 建立連接 {#section_B4D40CABDD3E46FDBE7B5651DFF91653}

>[!IMPORTANT]
>
>建立連接時不涉及瀏覽器TVSDK API。

要建立連接，發送方和接收方必須完成以下任務：

* 發件人必須在以下位置查看平台文檔： [發件人應用開發](https://developers.google.com/cast/docs/sender_apps)。
* 接收方使用Cast接收方API與發送方應用建立連接。 例如：

   ```js
   window.castReceiverManager = cast.receiver.CastReceiverManager.getInstance(); 
   
   window.castReceiverManager.onReady = function (event) { /*handle event*/ }; 
   window.castReceiverManager.onSenderConnected = function (event) { /*handle event*/ }; 
   window.castReceiverManager.onSenderDisconnected = function (event) { /*handle event*/ }; 
   
   var customMessageBus = window.castReceiverManager.getCastMessageBus(MSG_NAMESPACE); 
   customMessageBus.onMessage = function (event) { /*handle messages*/ }; 
   
   window.castReceiverManager.start(); 
   ```

## 消息處理 {#section_3E4814546F5946C9B3E7A1AE384B4FF8}

要向接收方發送消息，請參閱發送方平台的文檔。

>[!IMPORTANT]
>
>必須包括自定義消息命名空間， `MSG_NAMESPACE` 的下界。

對於接收器應用，請按照播放接收器API的文檔進行操作。

**基於Chrome的發件人消息示例**

```js
window.session.sendMessage(MSG_NAMESPACE, message, successCallback, errorCallback); //https://developers.google.com/cast/docs/reference/chrome/chrome.cast.Session#sendMessage
```

**基於Chrome的發件人事件處理**

將事件處理程式綁定到UI元素，這些元素將在觸發相應事件時發送消息。 例如，對於基於Chrome的發送程式應用，可能會發送以下查找事件：

```js
document.getElementById("#seekBar").addEventListener("click", seekEventHandler); 
   
function seekEventHandler(event) { 
    seekMessage = { type: "seek", seekTo: player.currentTime }; //player is an instance of AdobePSDK.MediaPlayer 
    window.session.sendMessage(MSG_NAMESPACE, seekMessage, successCallback, errorCallback); 
} 
```

**接收方消息處理**

在接收器應用中，下面是如何處理查找消息的示例：

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
