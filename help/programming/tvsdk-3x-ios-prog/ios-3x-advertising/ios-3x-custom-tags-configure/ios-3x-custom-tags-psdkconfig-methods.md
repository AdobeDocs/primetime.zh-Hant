---
description: 您可以使用PTSDKConfig類別在TVSDK中全域設定自訂標籤名稱。
title: 標籤的設定類別方法
exl-id: 017b766e-a6aa-4c14-af9a-2c88746e22c0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# 標籤的設定類別方法 {#config-class-methods-for-tags}

您可以使用PTSDKConfig類別在TVSDK中全域設定自訂標籤名稱。

TVSDK會自動將全域設定套用至未指定資料流特定設定的任何媒體資料流。

`PTSDKConfig` 公開這些方法來管理自訂標籤：

| **訂閱特定自訂標籤** |  |
|---|---|
| `subscribedTags` | 擷取訂閱標籤的目前清單。 |
| `setSubscribedTags` | 設定將公開給應用程式的訂閱標籤清單。 |
| **自訂預設機會偵測器使用的廣告標籤** |
| `adTags` | 擷取目前的廣告標籤清單。 |
| `setAdTags` | 設定預設機會產生器將使用的廣告標籤清單。 |


請記住以下事項：

* setter方法不允許tags引數包含null值。
* 自訂標籤名稱必須包含#首碼。

   例如，#EXT-X-ASSET是正確的自訂標籤名稱，但EXT-X-ASSET不正確。
* 媒體資料流載入後，您就無法變更設定。
