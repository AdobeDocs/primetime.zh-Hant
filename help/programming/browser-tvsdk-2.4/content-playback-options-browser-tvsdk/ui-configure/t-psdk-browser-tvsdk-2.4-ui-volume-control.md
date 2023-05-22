---
description: 可以設定聲音音量的用戶介面控制項。
title: 提供音量控制
exl-id: 5c446081-5491-46b6-9259-293131af80cb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '87'
ht-degree: 0%

---

# 提供音量控制{#provide-volume-control}

可以設定聲音音量的用戶介面控制項。

1. 等待 `MediaPlayer` 實例處於此命令的有效狀態。

   除RELEASED或ERROR之外的任何狀態都有效。
1. 在 `MediaPlayer` 實例，以設定音頻卷。

   ```js
   player.volume = ...
   ```

   卷的值表示請求的卷佔最大卷的比例，其中0為靜默，是最大卷。
