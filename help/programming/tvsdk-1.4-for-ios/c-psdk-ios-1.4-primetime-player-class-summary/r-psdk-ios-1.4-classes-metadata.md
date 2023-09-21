---
description: 這些類別提供廣告、名稱空間和追蹤的中繼資料。
title: 中繼資料類別
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 中繼資料類別{#metadata-classes}

這些類別提供廣告、名稱空間和追蹤的中繼資料。

| 名稱 | 說明 |
|---|---|
| [PTAdMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdMetadata.html) | 類別，提供解析指定媒體專案之廣告時應設定的屬性。 必須設定所有必要屬性，才能設定播放器以成功解析廣告。 |
| [PTAuditudeMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) | 擴充的類別 `PTAdMetadata` 專門用於Adobe Primetime ad decisioning。 提供針對指定媒體專案解析Adobe Primetime廣告決策廣告要設定的屬性。 您必須設定所有必要的屬性（包括區域ID、媒體ID和廣告伺服器URL），以設定播放器以成功解析廣告。 |
| [PTMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMetadata.html) | 定義基底類別，用於設定播放器和其他物件所有可用的中繼資料。 |
| [PTTimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTTimedMetadata.html) | 代表串流中自訂HLS標籤的類別。 |
| [PTTrackingMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTTrackingMetadata.html) | 定義所有追蹤和分析相關中繼資料的基底類別。 |
