---
description: 當VMAP內嵌廣告包含無效的媒體類型時，您可以啟用備援。
seo-description: 當VMAP內嵌廣告包含無效的媒體類型時，您可以啟用備援。
seo-title: 定義VMAP內嵌廣告的備援廣告行為
title: 定義VMAP內嵌廣告的備援廣告行為
uuid: a7b5c9a6-f546-4d3a-9d49-7e5484acff7a
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
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

