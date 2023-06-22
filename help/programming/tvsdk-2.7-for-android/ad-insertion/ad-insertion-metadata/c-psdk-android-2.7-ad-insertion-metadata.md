---
description: 為了讓廣告解析程式運作，廣告提供者(例如Adobe Primetime ad decisioning)需要設定值來啟用您與提供者的連線。
title: 廣告插入中繼資料
exl-id: fb78da4c-129e-4ecd-b598-3ab8af40d713
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# 概觀 {#ad-insertion-metadata-overview}

為了讓廣告解析程式運作，廣告提供者(例如Adobe Primetime ad decisioning)需要設定值來啟用您與提供者的連線。

TVSDK包含Primetime廣告決策程式庫。 若要讓您的內容包含來自Primetime ad decisioningserver的廣告，您的應用程式必須提供下列必要專案 `AuditudeSettings` 資訊：

* `mediaID`，此為要播放之視訊的唯一識別碼。

   發佈者在將視訊內容和廣告資訊提交至Adobe Primetime廣告決策伺服器時，會指派mediaID。 Primetime廣告決策會使用此ID從伺服器擷取視訊的相關廣告資訊。

* （可選） `defaultMediaId`，會指定在符合下列條件時提供的廣告：

   * 您對廣告伺服器的請求無效，或內容設定不正確。
   * Primetime ad decisioning在傳播資料時發生延遲。
   * 其中一個Primetime廣告決策後端程式發生問題或無法使用。

   >[!TIP]
   >
   >Adobe建議使用 `defaultMediaId`.

* 您的 `zoneID`由Adobe指派，可識別您的公司或網站。
* 您指派的廣告伺服器的網域。
* 其他目標定位引數。

   您可以根據自己的需求和廣告提供者的需求包含這些引數。
