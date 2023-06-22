---
description: 當VMAP內嵌廣告包含無效的媒體型別時，您可以啟用遞補。
title: 定義VMAP內嵌廣告的遞補廣告行為
exl-id: 57fd1b89-bcee-4c23-88e7-7a576c47c6f9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# 定義VMAP內嵌廣告的遞補廣告行為 {#define-fallback-ad-behavior-for-vmap-inline-ads}

當VMAP內嵌廣告包含無效的媒體型別時，您可以啟用遞補。

1. 設定 `setFallbackOnInvalidCreativeEnabled` 至 `true` 線性廣告/內嵌廣告的媒體型別對HLS無效時，讓VMAP後援。

   預設值為 `false`. 如果線性廣告因媒體型別無效或無法重新封裝而失敗，此標幟可讓Primetime廣告決策遵循相同的遞補行為，就像廣告是空的VAST包裝函式。

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```
