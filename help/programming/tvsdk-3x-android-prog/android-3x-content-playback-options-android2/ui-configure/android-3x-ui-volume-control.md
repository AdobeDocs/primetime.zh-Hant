---
description: 您可以設定用戶介面控制項來調整視頻的音量。
title: 提供音量控制
exl-id: 8b8b0263-9874-4e87-853e-eb394ebef3e3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# 提供音量控制 {#provide-volume-control}

您可以設定用戶介面控制項來調整視頻的音量。

1. 在卷控制介面元素的回調常式中，確保播放器處於此命令的有效狀態。

   >[!TIP]
   >
   >除RELEASED外的任何狀態都有效。

1. 呼叫 `setVolume` 來設定音頻音量。

   例如：

   ```java
   void setVolume(int volume) throws MediaPlayerException;
   ```

   卷的值表示請求的卷佔最大卷的比例，其中 `0` 安靜 `1` 是最大卷。
