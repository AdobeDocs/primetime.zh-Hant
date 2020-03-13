---
description: 您可以使用PTSDKConfig類別，在TVSDK中全域設定自訂標籤名稱。
seo-description: 您可以使用PTSDKConfig類別，在TVSDK中全域設定自訂標籤名稱。
seo-title: 標籤的Config類方法
title: 標籤的Config類方法
uuid: 1d3651a0-3b70-4d3a-8ced-663a9dad7205
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

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

