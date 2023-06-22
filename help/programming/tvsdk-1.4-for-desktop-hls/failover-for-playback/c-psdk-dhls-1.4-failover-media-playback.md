---
description: 對於即時和隨選影片(VOD)媒體，TVSDK會透過下載與中階解析度位元速率相關的播放清單來開始播放，並下載該播放清單定義的媒體區段。 它會快速選取高解析度位元速率播放清單及其相關媒體，並繼續下載程式。
title: 媒體播放和容錯移轉
exl-id: 43a44631-0b45-4f4e-8ec3-d3e1a0d5c71a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# 媒體播放和容錯移轉{#media-playback-and-failover}

對於即時和隨選影片(VOD)媒體，TVSDK會透過下載與中階解析度位元速率相關的播放清單來開始播放，並下載該播放清單定義的媒體區段。 它會快速選取高解析度位元速率播放清單及其相關媒體，並繼續下載程式。

## 缺少播放清單容錯移轉 {#section_E6B6A15930894F56A0A8501577B35E7F}

當整個播放清單遺失時，例如當頂層資訊清單檔案中指定的M3U8檔案未下載時，TVSDK會嘗試復原。 如果無法復原，您的應用程式會決定下一個步驟。

如果缺少與中間解析度位元速率相關聯的播放清單，TVSDK會搜尋具有相同解析度的變體播放清單。 如果找到相同的解析度，會開始從相符位置下載變體播放清單和區段。 如果TVSDK找不到相同解析度的播放清單，則會嘗試循環瀏覽其他位元速率播放清單及其變體。 立即較低的位元速率是第一個選擇，然後是它的變體，依此類推。 如果嘗試尋找有效播放清單時，所有較低位元速率的播放清單及其變體都已耗盡，TVSDK將會移至最高位元速率，並從此處開始計數。 如果找不到有效的播放清單，程式會失敗，播放器會變成ERROR狀態。

您的應用程式可決定如何處理這種情況。 例如，您可能想要關閉播放器活動，並將使用者導向目錄活動。 感興趣的事件是 `STATUS_CHANGED` 事件，而對應的回呼為 `onStatusChange` 方法。 以下是監控播放器是否將其內部狀態變更為錯誤的程式碼：

如需詳細資訊，請參閱 `PSDKDemo` 檔案。 事件接聽程式會附加至MediaPlayer執行個體。

```
case MediaPlayerStatus.ERROR: 
Alert.show(event.error.toString(), “Error occurred”); 
break;
```

如果使用者端網路已關閉，您可以使用此程式碼進行驗證。

```
psdkutils::PSDKString 
getNetworkDownVerificationUrl() const { return 
_networkDownVerificationUrl; }
```

API會提供用於驗證使用者端網路是否關閉的URL。 這應為有效的URL，會在http要求上傳回http回應代碼200。

```
psdkutils::PSDKErrorCode 
 setNetworkDownVerificationUrl(psdkutils::PSDKString value) {  
_networkDownVerificationUrl = value; return psdkutils::kECSuccess; }
```

如果未設定setNetworkDownVerificationUrl，TVSDK預設會使用MainManifest url來判斷網路是否關閉。

## 缺少區段容錯移轉 {#section_ED8CF666289042D39E9914D42BDD9BA4}

當區段遺失時，例如當特定區段下載失敗時，TVSDK會嘗試透過各種容錯移轉嘗試來復原。 如果無法復原，則會發出錯誤。

如果伺服器上缺少區段，例如，因為資訊清單檔案不存在、無法下載區段等，TVSDK會嘗試透過下列選項進行容錯移轉：

1. 嘗試以相同的位元速率容錯移轉至變體檔案中的相同區段。
1. 切換至相同檔案中的替代位元速率（ABR切換）。
1. 在每個可用的變體中，循環每個可用的位元速率。
1. 略過區段並發出警告。

當TVSDK無法取得替代區段時，就會觸發 `CONTENT_ERROR` 錯誤通知。 此通知包含程式碼的內部通知 `DOWNLOAD_ERROR` 程式碼。 如果問題的串流是替代音軌，TVSDK會產生 `AUDIO_TRACK_ERROR` 錯誤通知。

如果視訊引擎持續無法取得區段，則會將持續區段略過限製為5，之後會停止播放且TVSDK會發出 `NATIVE_ERROR` 程式碼為5。

>[!NOTE]
>
>發生容錯移轉時，不會考慮最適化位元速率(ABR)控制引數。 這是因為容錯移轉機制的設計是要使用任何目前可用的播放清單（不論其位元速率設定檔為何）作為備份串流。
>
>在容錯移轉作業期間，可以有一個設定檔交換器。 如果在下載其中一個播放清單區段期間發生錯誤，則會忽略ABR控制引數，例如最小/最大允許位元速率。
