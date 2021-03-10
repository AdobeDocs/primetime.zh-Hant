---
description: 當變型播放清單具有相同位元速率的多個轉譯，且其中一個轉譯停止運作時，就會發生容錯處理。 TVSDK會在轉譯之間切換。
title: 故障切換
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---


# 故障切換{#failover}

當變型播放清單具有相同位元速率的多個轉譯，且其中一個轉譯停止運作時，就會發生容錯處理。 TVSDK會在轉譯之間切換。

下列範例顯示具有相同位元速率之容錯移轉URL的變型播放清單：

```
#EXTM3U
#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8090/_default_/_default_/livestream.m3u8   

#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8091/_default_/_default_/livestream.m3u8
```

當TVSDK載入變型播放清單時，會建立佇列，以相同位元速率儲存內容所有轉譯的URL。 當請求URL失敗時，TVSDK會使用容錯佇列中相同位元速率的下一個URL。 在任何特定失敗時間，TVSDK都會循環使用一次所有可用的URL，直到找到可正常運作的URL，或直到嘗試所有可用的URL為止。 如果TVSDK已嘗試使用所有可用的URL，而且URL無法運作，TVSDK會停止嘗試播放內容。

故障切換僅發生在M3U8級別，這表示：

* 對於VOD，故障切換只有在嘗試播放時才會發生，在開始播放後不會發生。
* 對於即時串流，可在串流中間進行容錯。

>[!TIP]
>
>TVSDK提供容錯處理功能，而非Apple AV Foundation播放器。

