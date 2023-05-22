---
description: 當變型播放清單具有相同比特率的多個格式副本且其中一個格式副本停止工作時，將發生故障切換處理。 TVSDK在格式副本之間切換。
title: 故障轉移
exl-id: 8c215e2b-e601-4991-a66f-0e810176a511
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---

# 故障轉移{#failover}

當變型播放清單具有相同比特率的多個格式副本且其中一個格式副本停止工作時，將發生故障切換處理。 TVSDK在格式副本之間切換。

以下示例顯示了具有相同比特率的故障轉移URL的變型播放清單：

```
#EXTM3U
#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8090/_default_/_default_/livestream.m3u8   

#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8091/_default_/_default_/livestream.m3u8
```

當TVSDK載入變型播放清單時，它會建立一個隊列，該隊列以相同比特率保存內容的所有格式副本的URL。 當請求URL失敗時，TVSDK使用故障轉移隊列中的下一個相同比特率的URL。 在任何特定故障時間，TVSDK都會循環一次，直到找到一個正常工作的URL或嘗試了所有可用URL。 如果TVSDK已嘗試使用所有可用URL，但URL均不工作，則TVSDK將停止嘗試播放內容。

故障切換僅在M3U8級別進行，這意味著：

* 對於VOD ，只有在嘗試播放時才會發生故障切換，而不是在開始播放後。
* 對於即時流，可以在流的中間執行故障切換。

>[!TIP]
>
>TVSDK(而不是AppleAV Foundation播放器)提供故障轉移處理。
