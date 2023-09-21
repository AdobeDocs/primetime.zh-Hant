---
description: 部分協力廠商廣告（或創意）無法結合至HTTP即時資料流(HLS)內容串流，因為其視訊格式與HLS不相容。 Primetime廣告插入和TVSDK可選擇嘗試將不相容的廣告重新封裝為相容的M3U8影片。
title: 使用Adobe Creative重新封裝服務(CRS)重新封裝不相容的廣告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# 使用Adobe Creative重新封裝服務(CRS)重新封裝不相容的廣告 {#repackage-incompatible-ads-using-adobe-creative-repackaging-service-crs}

部分協力廠商廣告（或創意）無法結合至HTTP即時資料流(HLS)內容串流，因為其視訊格式與HLS不相容。 Primetime廣告插入和TVSDK可選擇嘗試將不相容的廣告重新封裝為相容的M3U8影片。

由不同協力廠商提供的廣告，例如代理商廣告伺服器、您的詳細目錄合作夥伴或廣告網路，通常會以不相容的格式傳送，例如漸進式下載MP4格式。

當TVSDK首次遇到不相容的廣告時，播放器會忽略該廣告並向Creative重新封裝服務(CRS) （這是Primetime廣告插入後端的一部分）發出請求，以將廣告重新封裝為相容格式。 CRS會嘗試產生廣告的多位元速率M3U8轉譯，並將這些轉譯儲存至Primetime內容傳遞網路(CDN)。 下次TVSDK收到指向該廣告的廣告回應時，播放器會使用來自CDN的HLS相容M3U8版本。

若要啟用此選用CRS功能，請聯絡您的Adobe代表。

>[!NOTE]
>
>對於CRS 3.0版（及舊版）客戶，從CRS 3.1版開始，下列變更已改善安全性和效能：
>
>* CRS 3.1繼續提供 `https:` 如果重新封裝的內容使用 `https:`. 如此一來，部分播放器呈現不安全內容的可能性就會降低。
>
>* CRS 3.1大幅減少網路呼叫，改善視訊啟動時間。
>

## 在TVSDK應用程式中啟用CRS {#enable-crs-in-tvsdk-applications}

若要在TVSDK應用程式中啟用CRS，您必須在Auditude設定中設定下列資訊：

1. 在中啟用CRS `AuditudeSettings`.

   ```
   ... 
   auditudeSettings.setCreativeRepackagingEnabled(true); 
   auditudeSettings.setCreativeRepackagingFormat("application/x-mpegURL"); 
   ```
