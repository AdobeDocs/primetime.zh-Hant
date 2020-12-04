---
description: 當VMAP內嵌廣告包含無效的媒體類型時，您可以啟用備援。
seo-description: 當VMAP內嵌廣告包含無效的媒體類型時，您可以啟用備援。
seo-title: 定義VMAP內嵌廣告的備援廣告行為
title: 定義VMAP內嵌廣告的備援廣告行為
uuid: bc8cb0b4-5ea9-429b-ab5d-746c6f03e74b
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---


# 定義VMAP內嵌廣告的備援廣告行為{#define-fallback-ad-behavior-for-vmap-inline-ads}

當VMAP內嵌廣告包含無效的媒體類型時，您可以啟用備援。

1. 將`setFallbackOnInvalidCreativeEnabled`設為`true`，當線性／內嵌廣告的媒體類型對HLS無效時，VMAP會回落。

   預設值為`false`。 如果線性廣告因為媒體類型無效或廣告無法重新封裝而失敗，則此標幟可讓Primetime廣告決策遵循與廣告為空的VAST包裝函式相同的備援行為。

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```
