---
description: 創造性重新打包服務(CRS)確保非HLS廣告創意可以在HLS流中正確回放。 清單伺服器在遇到非HLS廣告時調用CRS。
title: CRS概述
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---


# CRS概述 {#overview-of-crs}

創造性重新打包服務(CRS)確保非HLS廣告創意可以在HLS流中正確回放。 清單伺服器在遇到非HLS廣告時調用CRS。

>[!NOTE]
>
>預設情況下，CRS被禁用。 要為您的帳戶啟用CRS，請與Adobe技術客戶經理聯繫。
>
>有關在TVSDK應用中啟用CRS的資訊，請參見 *在TVSDK應用程式中啟用CRS* 平台的「程式設計師指南」中的主題。 例如，有關Android 3.4，請參見 [在TVSDK應用程式中啟用CRS](../../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-transcoding/android-3x-ad-transcoding.md)

CRS為內容流準備HTTP即時流(HLS)和創意，並為客戶端和跟蹤注入ID3資料包。 它將從第三方廣告伺服器、廣告網路和代理伺服器接收的MP4、FLV和WebM檔案轉換為HLS格式。

當Adobe Primetime的廣告插入遇到非HLS的廣告創意時，它會將廣告發到CRS進行重新打包，這通常不超過三分鐘。 CRS將轉碼和創意發送到CDN伺服器供將來使用。 這叫 **`just-in-time (JIT) repackaging`**。 您還可以在需要使用  [重新打包API](../../primetime-ad-insertion/~old-creative-repackaging-service/api-repackage.md) 。 這叫 *`asynchronous repackaging`*。

如果您的Adobe技術客戶經理還可以更改某些CRS預設行為，如果其他行為更適合您的應用程式。 這些是：

* 廣告創意格式的優先順序。

   的 `MediaFiles` VAST/VMAP響應的部分可以包含具有不同 `MediaFile` 的下界。 預設情況下，清單伺服器根據固定的優先順序集選擇一個( `application/x-mpegURL`。 `application/vnd.apple.mpegURL`。 `video/mp4`。 `video/x-flv,video/webm`)。 Adobe可以更改您帳戶的優先順序。
* 廣告目標持續時間。

   清單伺服器從內容播放清單中檢測目標和持續時間並將其發送到CRS。 Adobe可以更改此行為，以便CRS始終使用您為帳戶指定的固定持續時間。
