---
description: 您可以設定音量的使用者介面控制項。
title: 提供音量控制
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '87'
ht-degree: 0%

---


# 提供卷控制{#provide-volume-control}

您可以設定音量的使用者介面控制項。

1. 等待`MediaPlayer`實例處於該命令的有效狀態。

   除「已發佈」或「錯誤」以外的任何狀態都有效。
1. 在`MediaPlayer`實例上設定volume屬性以設定音頻卷。

   ```js
   player.volume = ...
   ```

   卷的值表示請求的卷佔最大卷的比例，其中0為靜默，是最大卷。

