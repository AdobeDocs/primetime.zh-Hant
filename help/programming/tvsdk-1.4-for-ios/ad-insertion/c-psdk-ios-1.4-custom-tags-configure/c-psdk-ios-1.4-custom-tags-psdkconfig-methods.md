---
description: 您可以使用PTSDKConfig類別，在TVSDK中全域設定自訂標籤名稱。
title: 標籤的Config類方法
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---


# 標籤的Config類方法{#config-class-methods-for-tags}

您可以使用PTSDKConfig類別，在TVSDK中全域設定自訂標籤名稱。

TVSDK會自動將全域組態套用至任何未指定串流特定組態的媒體串流。

`PTSDKConfig` 公開這些方法以管理自訂標籤：

| **訂閱特定的自訂標籤** |
|---|
| `subscribedTags` | 擷取目前訂閱標籤的清單。 |
| `setSubscribedTags` | 設定將公開至應用程式的訂閱標籤清單。 |
| **自訂預設機會偵測器使用的廣告標籤** |
| `adTags` | 擷取廣告標籤的目前清單。 |
| `setAdTags` | 設定預設業務機會生成器將使用的廣告標籤清單。 |

請記住：

* setter方法不允許標籤參數包含空值。
* 自訂標籤名稱必須包含#首碼。

   例如，#EXT-X-ASSET是正確的自訂標籤名稱，但EXT-X-ASSET不正確。
* 媒體串流載入後，您無法變更設定。

