---
description: 創意重新封裝服務(CRS)可確保非HLS廣告創意可以在HLS資料流中正確播放。 資訊清單伺服器遇到非HLS廣告時，會在CRS上呼叫。
title: CRS概觀
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---


# CRS概觀 {#overview-of-crs}

創意重新封裝服務(CRS)可確保非HLS廣告創意可以在HLS資料流中正確播放。 資訊清單伺服器遇到非HLS廣告時，會在CRS上呼叫。

>[!NOTE]
>
>CRS預設為停用。 若要啟用您帳戶的CRS，請聯絡您的Adobe技術客戶經理。
>
>如需在TVSDK應用程式中啟用CRS的詳細資訊，請參閱 *在TVSDK應用程式中啟用CRS* 適用於您平台的程式設計人員指南中的主題。 例如，若為Android 3.4，請參閱 [在TVSDK應用程式中啟用CRS](../../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-transcoding/android-3x-ad-transcoding.md)

CRS會為內容串流準備HTTP即時串流(HLS)廣告創意，並為使用者端廣告追蹤插入ID3封包。 它會將從協力廠商廣告伺服器、廣告網路和代理伺服器接收的MP4、FLV和WebM檔案轉碼為HLS格式。

當Adobe Primetime廣告插入遇到非HLS廣告創意時，它會將其傳送到CRS進行重新封裝，這通常不會超過三分鐘。 CRS會將轉碼廣告創意傳送至CDN伺服器以供日後使用。 這稱為 **`just-in-time (JIT) repackaging`**. 您也可以在需要使用廣告創意之前，透過以下方式將其轉碼  [重新封裝API](../../primetime-ad-insertion/~old-creative-repackaging-service/api-repackage.md) . 這稱為 *`asynchronous repackaging`*.

如果其他行為更適合您的應用程式，您的Adobe技術客戶經理也可以變更某些CRS預設行為。 這些功能包括：

* 廣告創意格式的優先順序。

   此 `MediaFiles` VAST/VMAP回應的區段可以包含具有不同特性的創意內容 `MediaFile` 型別。 依預設，資訊清單伺服器會根據一組固定的優先順序選取一個資訊清單( `application/x-mpegURL`， `application/vnd.apple.mpegURL`， `video/mp4`， `video/x-flv,video/webm`)。 Adobe可以變更您帳戶的優先順序。
* 廣告目標持續時間。

   資訊清單伺服器會從內容播放清單偵測目標廣告持續時間，並將其傳送至CRS。 Adobe可以變更此行為，讓CRS一律使用您為帳戶指定的固定持續時間。
