---
description: 某些協力廠商廣告（或創意素材）無法銜接至HTTP即時串流(HLS)內容串流，因為其視訊格式與HLS不相容。 Primetime廣告插入和TVSDK可選擇將不相容的廣告重新封裝至相容的M3U8視訊。
seo-description: 某些協力廠商廣告（或創意素材）無法銜接至HTTP即時串流(HLS)內容串流，因為其視訊格式與HLS不相容。 Primetime廣告插入和TVSDK可選擇將不相容的廣告重新封裝至相容的M3U8視訊。
seo-title: 使用Adobe Creative Repackaging Service(CRS)重新封裝不相容的廣告
title: 使用Adobe Creative Repackaging Service(CRS)重新封裝不相容的廣告
uuid: ef542d13-6d52-4429-8a1e-0af2df236f12
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 使用Adobe Creative Repackaging Service(CRS)重新封裝不相容的廣告 {#repackage-incompatible-ads-using-adobe-creative-repackaging-service-crs}

某些協力廠商廣告（或創意素材）無法銜接至HTTP即時串流(HLS)內容串流，因為其視訊格式與HLS不相容。 Primetime廣告插入和TVSDK可選擇將不相容的廣告重新封裝至相容的M3U8視訊。

來自不同第三方（例如代理商廣告伺服器、您的庫存合作夥伴或廣告網路）的廣告通常以不相容的格式提供，例如漸進式下載MP4格式。

當TVSDK第一次遇到不相容的廣告時，播放器會忽略廣告，並向創意重新封裝服務(CRS)發出請求，以將廣告重新封裝為相容格式。 CRS會嘗試產生廣告的多位元速率M3U8轉譯，並將這些轉譯儲存在Primetime內容傳送網路(CDN)上。 下次TVSDK收到指向該廣告的廣告回應時，播放器會從CDN使用HLS相容的M3U8版本。

若要啟用此選用的CRS功能，請連絡您的Adobe代表。

>[!NOTE]
>
>對於CRS 3.0版（及舊版）客戶，從CRS 3.1版開始，下列變更已改善安全性和效能：
>
>* CRS 3.1會繼續處理 `https:` 重新封裝的內容是否使用 `https:`。 這降低了某些播放器呈現不安全內容的可能性。
   >
   >
* CRS 3.1可大幅降低網路呼叫，縮短視訊啟動時間。

>



如需CRS的詳細資訊，請參 [閱Creative Packaging Service(CRS)](../../../../../dynamic-ad-insertion/creative-repackaging-service/crs-overview.md)。

## 在TVSDK應用程式中啟用CRS {#enable-crs-in-tvsdk-applications}

若要在TVSDK應用程式中啟用CRS，您必須在Auditude設定中設定下列資訊：

1. 在中啟用CRS `AuditudeSettings`。

   ```
   ... 
   auditudeSettings.setCreativeRepackagingEnabled(true); 
   auditudeSettings.setCreativeRepackagingFormat("application/x-mpegURL"); 
   ```
