---
description: 您可以設定使用者介面控制項，以調整視訊的音量。
seo-description: 您可以設定使用者介面控制項，以調整視訊的音量。
seo-title: 提供音量控制
title: 提供音量控制
uuid: f1e959e0-1817-4ccb-8adc-3eba09c91887
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 1%

---


# 提供卷控制{#provide-volume-control}

您可以設定使用者介面控制項，以調整視訊的音量。

1. 在卷控制介面元素的回呼常式中，確保播放器處於此命令的有效狀態。

   >[!TIP]
   >
   >除「已發佈」(RELEASED)外，任何狀態都有效。

1. 呼叫`setVolume`以設定音訊音量。

   例如：

   ```java
   void setVolume(int volume) throws MediaPlayerException;
   ```

   卷的值表示請求的卷佔最大卷的比例，其中`0`是靜默的，`1`是最大卷。

