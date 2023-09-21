---
description: 您可以設定使用者介面控制項來調整視訊的音量。
title: 提供音量控制
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# 提供音量控制 {#provide-volume-control}

您可以設定使用者介面控制項來調整視訊的音量。

1. 在音量控制介面元素的回呼常式中，確定播放器處於這個命令的有效狀態。

   >[!TIP]
   >
   >除了RELEASED之外，任何狀態都是有效的。

1. 呼叫 `setVolume` 設定音量。

   例如：

   ```java
   void setVolume(int volume) throws MediaPlayerException;
   ```

   磁碟區的值代表要求的磁碟區，以最大磁碟區的比例表示，其中 `0` 無訊息且 `1` 是最大數量。
