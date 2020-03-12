---
description: 您可以設定使用者介面控制項，以調整視訊的音量。
seo-description: 您可以設定使用者介面控制項，以調整視訊的音量。
seo-title: 提供音量控制
title: 提供音量控制
uuid: c87fe656-0329-4c9c-b65b-43be48c77062
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 提供音量控制 {#provide-volume-control}

您可以設定使用者介面控制項，以調整視訊的音量。

1. 在卷控制介面元素的回呼常式中，確保播放器處於此命令的有效狀態。

   >[!TIP]
   >
   >除「已發佈」外，任何狀態都有效。

1. 呼叫 `setVolume` 以設定音訊音量。

   例如：

   ```java
   void setVolume(int volume) throws MediaPlayerException;
   ```

   卷的值表示請求的卷佔最大卷的比例，其中 `0` 為靜默 `1` 和最大卷。