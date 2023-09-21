---
description: 您可以設定音量的使用者介面控制項。
title: 提供音量控制
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---

# 提供音量控制{#provide-volume-control}

您可以設定音量的使用者介面控制項。

1. 請等待MediaPlayer執行個體處於這個命令的有效狀態（RELEASED或ERROR以外的任何狀態）。
1. 呼叫 `setVolume` 於 `MediaPlayer` 執行個體以設定音量。

   ```java
   void setVolume(int volume) throws IllegalStateException;
   ```

   磁碟區的值代表要求的磁碟區，以最大磁碟區的比例表示，其中0是靜音，100是最大磁碟區。
