---
title: 傳遞內容
description: 傳遞內容
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# 傳遞內容 {#delivering-content}

Primetime DRM與內容的傳送機制無關，因為執行階段會抽象出網路層，而只是將受保護的內容提供給Primetime DRM子系統。 因此，可以透過HTTP、HTTP Dynamic Streaming、RTMP或RTMPE、HLS等傳遞內容。

不過，根據通訊協定，擷取受保護內容的中繼資料可能會很複雜( `DRMContentData`  — 通常採用側載的形式 [!DNL .metadata] 檔案)。 此DRM中繼資料是呼叫任何 `DRMManager` API，例如預先擷取授權、DRM驗證或加入裝置網域。 例如，使用RTMP/RTMPE通訊協定時，只有FLV和F4V資料可以透過Flash Media Server(FMS)傳遞給使用者端。 因此，使用者端必須透過其他方法擷取中繼資料blob。 解決此問題的一個選項是在HTTP網頁伺服器上託管中繼資料，並根據播放的內容實作使用者端視訊播放器以擷取適當的中繼資料。

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
