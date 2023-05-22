---
description: 某些第三方廣告（或創意）無法縫合到HTTP即時流(HLS)內容流中，因為其視頻格式與HLS不相容。 黃金時段廣告插入和TVSDK可以選擇嘗試將不相容的廣告重新打包到相容的M3U8視頻中。
title: 使用Adobe創意重新打包服務(CRS)重新打包不相容的廣告
exl-id: 7e1f9ffd-cd7e-488b-bbb7-f78e1623b697
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# 使用Adobe創意重新打包服務(CRS)重新打包不相容的廣告 {#repackage-incompatible-ads-using-adobe-creative-repackaging-service-crs}

某些第三方廣告（或創意）無法縫合到HTTP即時流(HLS)內容流中，因為其視頻格式與HLS不相容。 黃金時段廣告插入和TVSDK可以選擇嘗試將不相容的廣告重新打包到相容的M3U8視頻中。

來自不同第三方（如代理廣告伺服器、您的清單合作夥伴或廣告網路）的廣告通常以不相容的格式（如漸進式下載MP4格式）提供。

當TVSDK第一次遇到不相容的廣告時，播放器忽略該廣告並向作為黃金時段廣告插入後端的一部分的創造性重新打包服務(CRS)發出將該廣告重新打包成相容格式的請求。 CRS嘗試生成廣告的多比特率M3U8格式副本，並將這些格式副本儲存在黃金時段內容交付網路(CDN)上。 下次TVSDK收到指向該廣告的廣告響應時，播放器使用CDN中與HLS相容的M3U8版本。

要激活此可選CRS功能，請與Adobe代表聯繫。

>[!NOTE]
>
>對於CRS 3.0版（及更早版本）客戶，從CRS 3.1版開始，以下更改提高了安全性和效能：
>
>* CRS 3.1繼續 `https:` 如果要重新打包的內容使用 `https:`。 這降低了一些玩家呈現不安全內容的可能性。
>
>* CRS 3.1極大地減少了網路呼叫，縮短了視頻啟動時間。
>


## 在TVSDK應用程式中啟用CRS {#enable-crs-in-tvsdk-applications}

要在TVSDK應用程式中啟用CRS，必須在「審核」設定中設定以下資訊：

1. 在中啟用CRS `AuditudeSettings`。

   ```
   ... 
   auditudeSettings.setCreativeRepackagingEnabled(true); 
   auditudeSettings.setCreativeRepackagingFormat("application/x-mpegURL"); 
   ```
