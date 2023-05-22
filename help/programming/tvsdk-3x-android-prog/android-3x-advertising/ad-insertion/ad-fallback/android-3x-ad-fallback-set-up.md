---
description: 當VMAP內聯廣告包含無效的媒體類型時，可以啟用回退。
title: 定義VMAP內聯廣告的回退廣告行為
exl-id: 50de85b0-df2b-422f-893c-dfa641b4901e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# 定義VMAP內聯廣告的回退廣告行為 {#define-fallback-ad-behavior-for-vmap-inline-ads}

當VMAP內聯廣告包含無效的媒體類型時，可以啟用回退。

1. 設定 `setFallbackOnInvalidCreativeEnabled` 至 `true` 線上性/內聯ad的媒體類型對HLS無效時使VMAP回落。

   預設值為 `false`。 如果線性廣告因為其媒體類型無效或無法重新打包廣告而失敗，則此標誌允許Migna時廣告決策遵循與廣告是空的VAST包裝一樣的回退行為。

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```
