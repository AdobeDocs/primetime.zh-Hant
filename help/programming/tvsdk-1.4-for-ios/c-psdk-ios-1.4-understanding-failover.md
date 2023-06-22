---
description: 當變體播放清單中有多個相同位元速率的轉譯，且其中一個轉譯停止運作時，就會進行容錯移轉處理。 TVSDK會在轉譯之間切換。
title: 容錯移轉
exl-id: 8c215e2b-e601-4991-a66f-0e810176a511
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---

# 容錯移轉{#failover}

當變體播放清單中有多個相同位元速率的轉譯，且其中一個轉譯停止運作時，就會進行容錯移轉處理。 TVSDK會在轉譯之間切換。

以下範例顯示具有相同位元速率之容錯移轉URL的變體播放清單：

```
#EXTM3U
#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8090/_default_/_default_/livestream.m3u8   

#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8091/_default_/_default_/livestream.m3u8
```

當TVSDK載入變體播放清單時，它會建立一個佇列，以相同的位元速率儲存內容的所有轉譯的URL。 對URL的請求失敗時，TVSDK會使用容錯移轉佇列中具有相同位元速率的下一個URL。 TVSDK會在任何特定失敗時間，循環瀏覽所有可用的URL，直到找到運作正常的URL或嘗試使用所有可用的URL為止。 如果TVSDK嘗試了所有可用的URL，但所有URL都無法運作，則TVSDK會停止嘗試播放內容。

容錯移轉僅在M3U8層級進行，這表示：

* 對於VOD，容錯移轉只會在開始嘗試播放時發生，而不是在開始播放後發生。
* 對於即時串流，容錯移轉可能會發生在串流的中間。

>[!TIP]
>
>TVSDK (而非Apple AV Foundation播放器)提供容錯移轉處理功能。
