---
description: 您可以使用MediaPlayerItemConfig類別在TVSDK中全域設定自訂標籤名稱。
title: 標籤的設定類別方法
exl-id: 0a07ebdf-7336-4d4d-b7df-294afb3fd606
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# 標籤的設定類別方法 {#config-class-methods-for-tags}

您可以使用MediaPlayerItemConfig類別在TVSDK中全域設定自訂標籤名稱。

TVSDK會自動將全域設定套用至未指定資料流特定設定的任何媒體資料流。

`MediaPlayerItemConfig` 公開這些方法來管理自訂標籤：

**訂閱特定自訂標籤**

| <b>方法</b> | <b>說明</b> |
|--- |--- |
| `public final String[] getSubscribedTags` | 擷取訂閱標籤的目前清單。 |
| `public final void setSubscribedTags(String[] tags);` | 設定將公開給應用程式的訂閱標籤清單。  您的應用程式也會自動訂閱透過傳輸的所有標籤 `setAdTags`. |

**自訂預設機會偵測器使用的廣告標籤**

| <b>方法</b> | <b>說明</b> |
|--- |--- |
| `public final String[] getAdTags;` | 擷取目前的廣告標籤清單。 |
| `public final void setAdTags(String[] tags);` | 設定預設機會產生器將使用的廣告標籤清單。 |

請記住以下事項：

* setter方法不允許tags引數包含null值。

   如果發生，TVSDK會擲回 `IllegalArgumentException`.
* 自訂標籤名稱必須包含 `#` 前置詞。

   例如， `#EXT-X-ASSET` 是正確的自訂標籤名稱，但 `EXT-X-ASSET` 不正確。

* 媒體資料流載入後，您就無法變更設定。
