---
seo-title: 提供內容
title: 提供內容
uuid: b277d369-fee3-4a20-9dd8-27b3a8a82a9e
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# 提供內容 {#delivering-content}

Primetime DRM不受內容的傳送機制限制，因為執行時期會抽象出網路層，並僅將受保護的內容提供給Primetime DRM子系統。 因此，內容可透過HTTP、HTTP動態串流、RTMP或RTMPE、HLS等傳送。

不過，根據通訊協定，擷取受保護內容的中繼資料( `DRMContentData` 通常以側載檔案的形式)時可能會有複雜的 [!DNL .metadata] 處理。 需要此DRM中繼資料來呼叫任何 `DRMManager` API，例如預取授權、DRM驗證或加入裝置網域。 例如，使用RTMP/RTMPE通訊協定，只有FLV和F4V資料可透過Flash Media Server(FMS)傳送至用戶端。 因此，客戶端必須通過其他方法檢索元資料blob。 解決此問題的一個選項是將中繼資料裝載在HTTP網頁伺服器上，並實作用戶端視訊播放器，以擷取適當的中繼資料，視播放的內容而定。

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

