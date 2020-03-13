---
description: 您可以設定音量的使用者介面控制項。
seo-description: 您可以設定音量的使用者介面控制項。
seo-title: 提供音量控制
title: 提供音量控制
uuid: 5f2f69cc-3969-4ca2-8ab9-5713fdf5cdb8
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 提供音量控制{#provide-volume-control}

您可以設定音量的使用者介面控制項。

1. 等待實 `MediaPlayer` 例處於此命令的有效狀態。

   除「已發佈」或「錯誤」以外的任何狀態都有效。
1. 在實例上設定volume屬 `MediaPlayer` 性以設定音頻音量。

   ```js
   player.volume = ...
   ```

   卷的值表示請求的卷佔最大卷的比例，其中0為靜默，是最大卷。

