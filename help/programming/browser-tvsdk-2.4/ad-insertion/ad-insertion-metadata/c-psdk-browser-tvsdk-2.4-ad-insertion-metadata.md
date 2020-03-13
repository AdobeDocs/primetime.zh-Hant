---
description: 為了讓廣告解析程式運作，廣告提供者（例如Adobe Primetime廣告決策）需要設定值，才能啟用您與提供者的連線。
seo-description: 為了讓廣告解析程式運作，廣告提供者（例如Adobe Primetime廣告決策）需要設定值，才能啟用您與提供者的連線。
seo-title: 廣告插入中繼資料
title: 廣告插入中繼資料
uuid: 8848c939-1f12-4145-8025-453b4fe79aae
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 概觀 {#ad-insertion-metadata-overview}

為了讓廣告解析程式運作，廣告提供者（例如Adobe Primetime廣告決策）需要設定值，才能啟用您與提供者的連線。

瀏覽器TVSDK包含Adobe Primetime廣告決策程式庫。 若要讓您的內容包含來自Adobe Primetime廣告決策伺服器的廣告，您的應用程式必須提供下列必要的AuditudeSettings資訊：

* `mediaID`，這是要播放視訊的唯一識別碼。

   發佈者在將視訊內容和廣告資訊送出至Adobe Primetime廣告決策伺服器時，會指派mediaID。 Adobe Primetime廣告決策會使用此ID，從伺服器擷取視訊的相關廣告資訊。

* （可選） `defaultMediaId`，指定符合下列條件時提供的廣告：

   * 您對廣告伺服器的請求無效，或內容設定不正確。
   * Adobe Primetime廣告決策在傳播資料時遇到延誤。
   * 其中一個Adobe Primetime廣告決策後端程式運作不良或無法使用。
   >[!TIP]
   >
   >Adobe建議使用 `defaultMediaId`。

* 您 `zoneID`由Adobe指派的公司或網站識別。
* 您指派的廣告伺服器的網域。
* 其他定位參數。

   您可以根據您的需求和廣告提供者的需求，加入這些參數。