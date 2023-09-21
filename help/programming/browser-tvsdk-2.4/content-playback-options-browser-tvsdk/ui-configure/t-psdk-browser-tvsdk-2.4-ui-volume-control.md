---
description: 您可以設定音量的使用者介面控制項。
title: 提供音量控制
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '87'
ht-degree: 0%

---

# 提供音量控制{#provide-volume-control}

您可以設定音量的使用者介面控制項。

1. 等待 `MediaPlayer` 執行個體將處於此命令的有效狀態。

   除RELEASED或ERROR之外的任何狀態都是有效的。
1. 設定磁碟區屬性於 `MediaPlayer` 執行個體以設定音量。

   ```js
   player.volume = ...
   ```

   磁碟區的值代表要求的磁碟區，以最大磁碟區的比例表示，其中0是靜音的，而最大磁碟區是最大磁碟區。
