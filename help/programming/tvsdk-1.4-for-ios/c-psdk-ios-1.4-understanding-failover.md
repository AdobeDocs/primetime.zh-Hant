---
description: 當變體播放清單中有多個相同位元速率的轉譯，且其中一個轉譯停止運作時，就會進行容錯移轉處理。 TVSDK會在轉譯之間切換。
title: 容錯移轉
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---

# 容錯移轉{#failover}

當變體播放清單中有多個相同位元速率的轉譯，且其中一個轉譯停止運作時，就會進行容錯移轉處理。 TVSDK會在轉譯之間切換。

下列範例顯示具有相同位元速率之容錯移轉URL的變體播放清單：

```
#EXTM3U
#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8090/_default_/_default_/livestream.m3u8   

#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8091/_default_/_default_/livestream.m3u8
```

TVSDK載入變體播放清單時，會建立佇列，以相同位元速率儲存內容所有轉譯的URL。 當URL的請求失敗時，TVSDK會使用容錯移轉佇列中具有相同位元速率的下一個URL。 TVSDK會在任何特定失敗時間循環瀏覽所有可用的URL，直到找到運作正常的URL或嘗試所有可用的URL為止。 如果TVSDK已嘗試所有可用的URL但所有URL都無法運作，則TVSDK會停止嘗試播放內容。

容錯移轉僅在M3U8層級進行，這表示：

* 對於VOD，只有在開始嘗試播放時，才能進行容錯移轉，而不是在開始播放之後。
* 對於即時串流，容錯移轉可能會發生在串流中央。

>[!TIP]
>
>TVSDK (而非Apple AV Foundation播放器)提供容錯移轉處理功能。
