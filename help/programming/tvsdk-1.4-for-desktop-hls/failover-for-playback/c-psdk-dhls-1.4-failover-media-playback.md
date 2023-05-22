---
description: 對於即時和視頻點播(VOD)媒體，TVSDK通過下載與中解析度比特率相關聯的播放清單開始播放並下載由該播放清單定義的媒體段。 它快速選擇高解析度比特率播放清單及其相關媒體並繼續下載過程。
title: 媒體播放和故障切換
exl-id: 43a44631-0b45-4f4e-8ec3-d3e1a0d5c71a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# 媒體播放和故障切換{#media-playback-and-failover}

對於即時和視頻點播(VOD)媒體，TVSDK通過下載與中解析度比特率相關聯的播放清單開始播放並下載由該播放清單定義的媒體段。 它快速選擇高解析度比特率播放清單及其相關媒體並繼續下載過程。

## 缺少播放清單故障轉移 {#section_E6B6A15930894F56A0A8501577B35E7F}

當缺少整個播放清單時，例如，當在頂級清單檔案中指定的M3U8檔案未下載時，TVSDK會嘗試恢復。 如果無法恢復，則應用程式將確定下一步。

如果缺少與中解析度位速率關聯的播放清單，TVSDK將搜索相同解析度的變型播放清單。 如果找到相同的解析度，則開始從匹配位置下載變型播放清單和段。 如果TVSDK找不到相同的解析度播放清單，它將嘗試循環播放其他比特率播放清單及其變體。 立即降低比特率是首選，然後是其變數，等等。 如果在嘗試查找有效播放清單時已用盡所有低比特率播放清單及其變體，則TVSDK將轉到最高比特率並從那裡計算下來。 如果找不到有效的播放清單，則進程將失敗，並且播放器將移到ERROR狀態。

您的應用程式可以確定如何處理此情況。 例如，您可能希望關閉播放器活動並將用戶引導到目錄活動。 感興趣的事件是 `STATUS_CHANGED` 事件，相應的回調是 `onStatusChange` 的雙曲餘切值。 下面是代碼，用於監視播放器是否將其內部狀態更改為ERROR:

有關詳細資訊，請參見 `PSDKDemo` 的子菜單。 事件偵聽器已附加到MediaPlayer實例。

```
case MediaPlayerStatus.ERROR: 
Alert.show(event.error.toString(), “Error occurred”); 
break;
```

如果客戶端網路已關閉，則可以使用此代碼進行驗證。

```
psdkutils::PSDKString 
getNetworkDownVerificationUrl() const { return 
_networkDownVerificationUrl; }
```

API將提供用於驗證客戶端網路是否關閉的url。 這應該是有效的url，它在http請求上返回http響應代碼200。

```
psdkutils::PSDKErrorCode 
 setNetworkDownVerificationUrl(psdkutils::PSDKString value) {  
_networkDownVerificationUrl = value; return psdkutils::kECSuccess; }
```

如果未設定setNetworkDownVerificationUrl，則TVSDK預設使用MainManifest URL來確定網路是否關閉。

## 缺少段故障轉移 {#section_ED8CF666289042D39E9914D42BDD9BA4}

當缺少段時，例如，當特定段無法下載時，TVSDK會嘗試通過各種故障轉移嘗試進行恢復。 如果無法恢復，則會發出錯誤。

如果伺服器上缺少段，因為（例如）清單檔案不存在、無法下載段等，則TVSDK會嘗試使用以下選項來嘗試故障轉移：

1. 嘗試在變型檔案中以相同比特率故障切換到同一段。
1. 切換到同一檔案中的備用位速率（ABR交換機）。
1. 循環查看每個可用變數中的每個可用比特率。
1. 跳過段並發出警告。

當TVSDK無法獲取替代段時，它將觸發 `CONTENT_ERROR` 錯誤通知。 此通知包含包含代碼的內部通知 `DOWNLOAD_ERROR` 代碼。 如果出現問題的流是備用音頻軌道，TVSDK將生成 `AUDIO_TRACK_ERROR` 錯誤通知。

如果視頻引擎連續無法獲取段，它將連續段跳轉限制為5，然後停止播放，TVSDK發出 `NATIVE_ERROR` 5號密碼。

>[!NOTE]
>
>在發生故障切換時，不考慮自適應比特率(ABR)控制參數。 這是因為故障切換機制設計為將當前可用的任何播放清單用作備份流，而不管其比特率配置檔案如何。
>
>在故障轉移操作期間，可以有一個配置式交換機。 如果在下載其中一個播放清單段期間發生錯誤，則忽略ABR控制參數，如允許的最小/最大比特率。
