---
description: 可以使用MediaPlayerItemConfig類在TVSDK中全局配置自定義標籤名稱。
title: 標籤的Config類方法
exl-id: 0a07ebdf-7336-4d4d-b7df-294afb3fd606
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# 標籤的Config類方法 {#config-class-methods-for-tags}

可以使用MediaPlayerItemConfig類在TVSDK中全局配置自定義標籤名稱。

TVSDK自動將全局配置應用於未指定流特定配置的任何媒體流。

`MediaPlayerItemConfig` 公開了以下用於管理自定義標籤的方法：

**訂閱特定自定義標籤**

| <b>方法</b> | <b>說明</b> |
|--- |--- |
| `public final String[] getSubscribedTags` | 檢索當前訂閱標籤清單。 |
| `public final void setSubscribedTags(String[] tags);` | 設定將公開給應用程式的訂閱標籤清單。  您的應用程式還自動訂閱通過傳輸的所有標籤 `setAdTags`。 |

**自定義預設機會檢測器使用的廣告標籤**

| <b>方法</b> | <b>說明</b> |
|--- |--- |
| `public final String[] getAdTags;` | 檢索廣告標籤的當前清單。 |
| `public final void setAdTags(String[] tags);` | 設定預設機會生成器將使用的廣告標籤清單。 |

請記住以下內容：

* setter方法不允許標籤參數包含空值。

   如果遇到，TVSDK將引發 `IllegalArgumentException`。
* 自定義標籤名稱必須包含 `#` 前置詞。

   比如說， `#EXT-X-ASSET` 是正確的自定義標籤名稱，但 `EXT-X-ASSET` 不正確。

* 在載入媒體流後，不能更改配置。
