---
description: 對於即時和隨選視訊(VOD)媒體，TVSDK會下載與中解析度位元速率相關的播放清單，並下載該播放清單所定義的媒體區段，以開始播放。 它快速選擇高解析度位元速率播放清單及其相關媒體，並繼續下載程式。
title: 媒體播放和故障切換
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---


# 媒體播放和故障切換{#media-playback-and-failover}

對於即時和隨選視訊(VOD)媒體，TVSDK會下載與中解析度位元速率相關的播放清單，並下載該播放清單所定義的媒體區段，以開始播放。 它快速選擇高解析度位元速率播放清單及其相關媒體，並繼續下載程式。

## 缺少播放清單故障切換{#section_E6B6A15930894F56A0A8501577B35E7F}

例如，當整個播放清單遺失時，當頂層資訊清單檔案中指定的M3U8檔案未下載時，TVSDK會嘗試復原。 如果無法復原，您的應用程式會決定下一個步驟。

如果遺失與中解析度位元速率相關聯的播放清單，TVSDK會以相同解析度搜尋變型播放清單。 如果找到相同的解析度，就會開始從相符位置下載變型播放清單和區段。 如果TVSDK找不到相同的解析度播放清單，它會嘗試循環檢視其他位元速率播放清單及其變數。 位元速率立即降低是首選，然後是其變體，依此類推。 如果所有較低位元速率的播放清單及其變數在嘗試尋找有效播放清單時已用盡，TVSDK會移至最高位元速率，並從此計算。 如果找不到有效的播放清單，程式會失敗，而播放器會移至ERROR狀態。

您的應用程式可判斷如何處理此情況。 例如，您可能想要關閉播放器活動，並將使用者導向目錄活動。 感興趣的事件是`STATUS_CHANGED`事件，而對應的回呼是`onStatusChange`方法。 以下程式碼會監視播放器是否將內部狀態變更為ERROR:

如需詳細資訊，請參閱`PSDKDemo`檔案。 事件偵聽器被附加到MediaPlayer實例。

```
case MediaPlayerStatus.ERROR: 
Alert.show(event.error.toString(), “Error occurred”); 
break;
```

如果客戶端網路關閉，您可以使用此代碼進行驗證。

```
psdkutils::PSDKString 
getNetworkDownVerificationUrl() const { return 
_networkDownVerificationUrl; }
```

API將提供用於驗證客戶端網路是否關閉的URL。 此URL應為有效的URL，會在http請求上傳回http回應代碼200。

```
psdkutils::PSDKErrorCode 
 setNetworkDownVerificationUrl(psdkutils::PSDKString value) {  
_networkDownVerificationUrl = value; return psdkutils::kECSuccess; }
```

如果未設定setNetworkDownVerificationUrl,TVSDK會依預設使用MainManifest URL來判斷網路是否關閉。

## 缺少段故障切換{#section_ED8CF666289042D39E9914D42BDD9BA4}

當區段遺失時（例如，當特定區段無法下載時）,TVSDK會嘗試透過多種容錯嘗試進行復原。 如果無法恢復，則會發出錯誤。

如果伺服器上遺失區段，例如資訊清單檔案不存在、無法下載區段等，TVSDK會嘗試透過下列選項進行故障切換：

1. 嘗試在變型檔案中以相同位速率故障切換到同一段。
1. 在同一檔案中切換到備用位速率（ABR交換機）。
1. 循環檢視每個可用變數中的每個可用位元速率。
1. 略過區段並發出警告。

當TVSDK無法取得替代區段時，會觸發`CONTENT_ERROR`錯誤通知。 此通知包含內部通知，內含代碼`DOWNLOAD_ERROR`代碼。 如果出現問題的串流是替代音軌，TVSDK會產生`AUDIO_TRACK_ERROR`錯誤通知。

如果視訊引擎持續無法取得區段，會將連續區段跳至5，之後停止播放，TVSDK會發出代碼5的`NATIVE_ERROR`。

>[!NOTE]
>
>當故障切換發生時，不考慮自適應位速率(ABR)控制參數。 這是因為故障切換機制設計為使用任何當前可用的播放清單（無論其比特率配置檔案）作為備份流。
>
>在故障切換操作期間，可以有一個配置式交換機。 如果在下載其中一個播放清單區段期間發生錯誤，則會忽略ABR控制參數，例如允許的最小／最大位元速率。

