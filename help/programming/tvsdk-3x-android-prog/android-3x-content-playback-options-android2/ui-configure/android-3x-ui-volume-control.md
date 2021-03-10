---
description: 您可以設定使用者介面控制項，以調整視訊的音量。
title: 提供音量控制
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 2%

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