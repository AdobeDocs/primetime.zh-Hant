---
description: 您可以設定音量的使用者介面控制項。
title: 提供音量控制
exl-id: 5c446081-5491-46b6-9259-293131af80cb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '87'
ht-degree: 0%

---

# 提供音量控制{#provide-volume-control}

您可以設定音量的使用者介面控制項。

1. 等候 `MediaPlayer` 執行個體將處於此命令的有效狀態。

   除RELEASED或ERROR以外的任何狀態都有效。
1. 設定磁碟區屬性 `MediaPlayer` 執行個體以設定音量。

   ```js
   player.volume = ...
   ```

   磁碟區的值代表要求的磁碟區，以最大磁碟區的比例表示，其中0是靜音，是最大磁碟區。
