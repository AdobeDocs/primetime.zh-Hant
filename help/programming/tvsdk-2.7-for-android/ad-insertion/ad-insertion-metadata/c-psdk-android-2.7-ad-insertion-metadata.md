---
description: 為了讓廣告解析程式運作，廣告提供者（例如Adobe Primetime廣告決策）需要設定值，才能啟用您與提供者的連線。
seo-description: 為了讓廣告解析程式運作，廣告提供者（例如Adobe Primetime廣告決策）需要設定值，才能啟用您與提供者的連線。
seo-title: 廣告插入中繼資料
title: 廣告插入中繼資料
uuid: ee4dd8b8-4c41-4f01-be50-60f4c7dc962d
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---


# 概述{#ad-insertion-metadata-overview}

為了讓廣告解析程式運作，廣告提供者（例如Adobe Primetime廣告決策）需要設定值，才能啟用您與提供者的連線。

TVSDK包含Primetime廣告決策庫。 您的內容若要包含來自Primetime廣告決策伺服器的廣告，您的應用程式必須提供下列必要的`AuditudeSettings`資訊：

* `mediaID`，這是要播放視訊的唯一識別碼。

   發佈者在將視訊內容和廣告資訊送出至Adobe Primetime廣告決策伺服器時，會指派mediaID。 Primetime廣告決策會使用此ID，從伺服器擷取視訊的相關廣告資訊。

* （可選）`defaultMediaId`，指定符合下列條件時所提供的廣告：

   * 您對廣告伺服器的請求無效，或內容設定不正確。
   * Primetime廣告決策在傳播資料時遇到延遲。
   * Primetime廣告決策後端程式之一發生故障或不可用。

   >[!TIP]
   >
   >Adobe建議使用`defaultMediaId`。

* 由Adobe指派的`zoneID`可識別您的公司或網站。
* 您指派的廣告伺服器的網域。
* 其他定位參數。

   您可以根據您的需求和廣告提供者的需求，加入這些參數。