---
title: 傳遞內容
description: 傳遞內容
copied-description: true
exl-id: a55293f0-ef9b-468f-a1b2-8222ebab0b4b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# 傳遞內容 {#delivering-content}

Primetime DRM與內容的傳遞機制無關，因為執行階段會抽象出網路層，並僅將受保護的內容提供給Primetime DRM子系統。 因此，內容可以透過HTTP、HTTP Dynamic Streaming、RTMP或RTMPE、HLS等傳送。

不過，根據通訊協定，擷取受保護內容的中繼資料可能會涉及錯綜複雜的問題( `DRMContentData`  — 通常採用側載的形式 [!DNL .metadata] 檔案)。 此DRM中繼資料是呼叫任何 `DRMManager` API，例如預先擷取授權、DRM驗證或加入裝置網域。 例如，使用RTMP/RTMPE通訊協定時，只有FLV和F4V資料可以透過Flash Media Server(FMS)傳遞給使用者端。 因此，使用者端必須以其他方式擷取中繼資料blob。 解決此問題的一個選項是在HTTP網頁伺服器上託管中繼資料，並實作使用者端視訊播放器以擷取適當的中繼資料（視播放的內容而定）。

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
