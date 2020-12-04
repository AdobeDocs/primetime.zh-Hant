---
description: 您可以使用MediaPlayerItemConfig類別，在TVSDK中全域設定自訂標籤名稱。
seo-description: 您可以使用MediaPlayerItemConfig類別，在TVSDK中全域設定自訂標籤名稱。
seo-title: 標籤的Config類方法
title: 標籤的Config類方法
uuid: b75aebac-4b94-4c42-bed4-3c17ad989cd1
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# 標籤{#config-class-methods-for-tags}的Config類方法

您可以使用MediaPlayerItemConfig類別，在TVSDK中全域設定自訂標籤名稱。

TVSDK會自動將全域組態套用至任何未指定串流特定組態的媒體串流。

`MediaPlayerItemConfig` 公開這些方法以管理自訂標籤：

**訂閱特定的自訂標籤**

| <b>方法</b> | <b>說明</b> |
|--- |--- |
| `public final String[] getSubscribedTags` | 擷取目前訂閱標籤的清單。 |
| `public final void setSubscribedTags(String[] tags);` | 設定將公開至應用程式的訂閱標籤清單。  您的應用程式也會自動訂閱透過`setAdTags`傳輸的所有標籤。 |

**自訂預設機會偵測器使用的廣告標籤**

| <b>方法</b> | <b>說明</b> |
|--- |--- |
| `public final String[] getAdTags;` | 擷取廣告標籤的目前清單。 |
| `public final void setAdTags(String[] tags);` | 設定預設業務機會生成器將使用的廣告標籤清單。 |

請記住：

* setter方法不允許標籤參數包含空值。

   如果遇到此問題，TVSDK會拋出`IllegalArgumentException`。
* 自訂標籤名稱必須包含`#`首碼。

   例如，`#EXT-X-ASSET`是正確的自訂標籤名稱，但`EXT-X-ASSET`不正確。

* 媒體串流載入後，您無法變更設定。