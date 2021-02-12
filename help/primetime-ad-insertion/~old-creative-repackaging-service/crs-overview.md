---
description: 創意重新封裝服務(CRS)可確保非HLS廣告創意素材可在HLS串流中正確播放。 資訊清單伺服器在遇到非HLS廣告時會呼叫CRS。
seo-description: 創意重新封裝服務(CRS)可確保非HLS廣告創意素材可在HLS串流中正確播放。 資訊清單伺服器在遇到非HLS廣告時會呼叫CRS。
seo-title: CRS概觀
title: CRS概觀
uuid: 3ae75fa7-397f-47ba-8e3d-50543ca25458
translation-type: tm+mt
source-git-commit: e1e33d3ac0aad44859cd49566331524da72ac7e4
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---


# CRS {#overview-of-crs}概觀

創意重新封裝服務(CRS)可確保非HLS廣告創意素材可在HLS串流中正確播放。 資訊清單伺服器在遇到非HLS廣告時會呼叫CRS。

>[!NOTE]
>
>依預設，CRS會停用。 若要啟用您帳戶的CRS，請連絡您的Adobe技術帳戶管理員。
>
>如需在TVSDK應用程式中啟用CRS的詳細資訊，請參閱您平台的程式設計人員指南中的&#x200B;*在TVSDK應用程式中啟用CRS*&#x200B;主題。 例如，若是Android 3.4，請參閱[在TVSDK應用程式中啟用CRS](../../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-transcoding/android-3x-ad-transcoding.md)

CRS會針對內容串流準備HTTP即時串流(HLS)廣告創意，並插入ID3封包以用於用戶端廣告追蹤。 它會將從協力廠商廣告伺服器、廣告網路和機構伺服器收到的MP4、FLV和WebM檔案轉碼為HLS格式。

當Adobe Primetime廣告插入遇到非HLS廣告創意素材時，會將廣告傳送至CRS進行重新封裝，通常不超過三分鐘。 CRS會將轉碼廣告創意傳送至CDN伺服器，以供日後使用。 這稱為&#x200B;**`just-in-time (JIT) repackaging`**。 您也可以使用[重新封裝API](../../primetime-ad-insertion/~old-creative-repackaging-service/api-repackage.md)，在廣告創意素材需要之前先轉碼。 這稱為&#x200B;*`asynchronous repackaging`*。

如果您的Adobe技術帳戶管理員也可以變更某些CRS預設行為（如果其他行為更適合您的應用程式）。 以下是：

* 廣告創意格式的優先順序。

   VAST/VMAP回應的`MediaFiles`區段可包含不同`MediaFile`類型的創作元素。 根據預設，資訊清單伺服器會根據一組固定的優先順序(`application/x-mpegURL`、`application/vnd.apple.mpegURL`、`video/mp4`、`video/x-flv,video/webm`)來選擇一個。 Adobe可以變更您帳戶的優先順序。
* 廣告目標持續時間。

   資訊清單伺服器從內容播放清單中偵測目標廣告持續時間，並將其傳送至CRS。 Adobe可以變更此行為，讓CRS永遠使用您為帳戶指定的固定期間。
