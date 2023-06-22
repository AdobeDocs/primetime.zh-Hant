---
description: 您可以設定使用者介面控制項來調整視訊的音量。
title: 提供音量控制
exl-id: 8b8b0263-9874-4e87-853e-eb394ebef3e3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# 提供音量控制 {#provide-volume-control}

您可以設定使用者介面控制項來調整視訊的音量。

1. 在音量控制介面元素的回呼常式中，確定播放器處於這個命令的有效狀態。

   >[!TIP]
   >
   >除「已核發」以外的任何狀態都有效。

1. 呼叫 `setVolume` 設定音量。

   例如：

   ```java
   void setVolume(int volume) throws MediaPlayerException;
   ```

   磁碟區的值代表要求的磁碟區，以最大磁碟區的比例表示，其中 `0` 是靜音且 `1` 是最大磁碟區。
