---
description: 部分協力廠商廣告（或創意）無法結合至HTTP即時串流(HLS)內容資料流，因為其視訊格式與HLS不相容。 Primetime廣告插入和TVSDK可選擇嘗試將不相容的廣告重新封裝成相容的M3U8影片。
title: 使用Adobe Creative重新封裝服務(CRS)重新封裝不相容的廣告
exl-id: b6fb2846-64b6-4db7-a6a9-f85365780775
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# 使用Adobe Creative重新封裝服務(CRS)重新封裝不相容的廣告 {#repackage-incompatible-ads-using-adobe-creative-repackaging-service-crs}

部分協力廠商廣告（或創意）無法結合至HTTP即時串流(HLS)內容資料流，因為其視訊格式與HLS不相容。 Primetime廣告插入和TVSDK可選擇嘗試將不相容的廣告重新封裝成相容的M3U8影片。

由不同第三方提供的廣告，例如代理廣告伺服器、詳細目錄合作夥伴或廣告網路，通常以不相容的格式傳送，例如漸進式下載MP4格式。

當TVSDK首次遇到不相容的廣告時，播放器會忽略該廣告，並向創意重新封裝服務(CRS) （Primetime廣告插入後端的一部分）發出請求，以將廣告重新封裝為相容的格式。 CRS會嘗試產生廣告的多位元速率M3U8轉譯，並將這些轉譯儲存在Primetime內容傳遞網路(CDN)上。 下次TVSDK收到指向該廣告的廣告回應時，播放器會使用來自CDN的HLS相容M3U8版本。

若要啟用此選擇性CRS功能，請聯絡您的Adobe代表。

>[!NOTE]
>
>對於CRS 3.0版（及舊版）客戶，從CRS 3.1版開始，下列變更已改善安全性和效能：
>
>* CRS 3.1繼續提供 `https:` 如果重新封裝的內容使用 `https:`. 如此一來，部分播放器就不太可能呈現不安全的內容。
>
>* CRS 3.1大幅減少網路呼叫，改善視訊啟動時間。
>


如需CRS的詳細資訊，請參閱 [Creative Packaging Service (CRS)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_certificate_enrollment.pdf).

## 在TVSDK應用程式中啟用CRS{#enable-crs-in-tvsdk-applications}

若要在TVSDK應用程式中啟用CRS，您必須在稽核設定中設定下列資訊：

1. 在中啟用CRS `AuditudeSettings`.

   ```
   ... 
   auditudeSettings.setCreativeRepackagingEnabled(true); 
   auditudeSettings.setCreativeRepackagingFormat("application/x-mpegURL"); 
   ```
