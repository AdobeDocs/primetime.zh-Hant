---
description: 可以使用PTSDKConfig類全局配置TVSDK中的自定義標籤名稱。
title: 標籤的Config類方法
exl-id: 017b766e-a6aa-4c14-af9a-2c88746e22c0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# 標籤的Config類方法 {#config-class-methods-for-tags}

可以使用PTSDKConfig類全局配置TVSDK中的自定義標籤名稱。

TVSDK自動將全局配置應用於未指定流特定配置的任何媒體流。

`PTSDKConfig` 公開了以下用於管理自定義標籤的方法：

| **訂閱特定自定義標籤** |  |
|---|---|
| `subscribedTags` | 檢索當前訂閱標籤清單。 |
| `setSubscribedTags` | 設定將公開給應用程式的訂閱標籤清單。 |
| **自定義預設機會檢測器使用的廣告標籤** |
| `adTags` | 檢索廣告標籤的當前清單。 |
| `setAdTags` | 設定預設機會生成器將使用的廣告標籤清單。 |


請記住以下內容：

* setter方法不允許標籤參數包含空值。
* 自定義標籤名稱必須包含#前置詞。

   例如，#EXT-X-ASSET是正確的自定義標籤名稱，但EXT-X-ASSET不正確。
* 在載入媒體流後，不能更改配置。
