---
title: 提供內容
description: 提供內容
copied-description: true
exl-id: a55293f0-ef9b-468f-a1b2-8222ebab0b4b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# 提供內容 {#delivering-content}

黃金時段DRM對內容的傳送機制是不可知的，因為運行時將網路層抽象出來，並且僅將受保護的內容提供給黃金時段DRM子系統。 因此，內容可以通過HTTP、HTTP Dynamic Streaming、RTMP或RTMPE、HLS等來傳送。

但是，根據協定的不同，檢索受保護內容的元資料可能涉及複雜的內容( `DRMContentData`  — 通常以側裝的形式 [!DNL .metadata] )。 需要此DRM元資料來調用任何 `DRMManager` API，例如預取許可證、DRM驗證或加入設備域。 例如，使用RTMP/RTMPE協定，只有FLV和F4V資料可以通過Flash Media Server(FMS)傳送到客戶端。 因此，客戶端必須通過其他方式檢索元資料blob。 解決此問題的一個選項是將元資料托管在HTTP Web伺服器上，並實施客戶端視頻播放器以根據正在回放的內容檢索相應的元資料。

```
private function getMetadata():void { 
    extrapolated-path-to-metadata = "https://metadatas.mywebserver.com/" + videoname; 
     var urlRequest : URLRequest =  
      new URLRequest(extrapolated-path-to-the-metadata + ".metadata");  
    var urlStream : URLStream = new URLStream();  
    urlStream.addEventListener(Event.COMPLETE, handleMetadata);  
    urlStream.addEventListener(IOErrorEvent.NETWORK_ERROR, handleIOError);  
    urlStream.addEventListener(IOErrorEvent.IO_ERROR, handleIOError);  
    urlStream.addEventListener(IOErrorEvent.VERIFY_ERROR, handleIOError);  
 
    try { 
        urlStream.load(urlRequest);  
    } catch(se:SecurityError) { 
        videoLog.text += se.toString() + "\n";  
    } catch(e:Error) { 
        videoLog.text += e.toString() + "\n";  
    } 
} 
```
