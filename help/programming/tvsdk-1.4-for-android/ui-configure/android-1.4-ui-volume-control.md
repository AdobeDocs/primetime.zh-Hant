---
description: 您可以設定音量的使用者介面控制項。
title: 提供音量控制
exl-id: aa8ffdf3-515b-4899-8a00-8fb5b8c595a9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---

# 提供音量控制{#provide-volume-control}

您可以設定音量的使用者介面控制項。

1. 請等待MediaPlayer執行個體處於這個命令的有效狀態（除了RELEASED或ERROR之外）。
1. 呼叫 `setVolume` 於 `MediaPlayer` 執行個體以設定音量。

   ```java
   void setVolume(int volume) throws IllegalStateException;
   ```

   磁碟區的值代表要求的磁碟區，以最大磁碟區的比例表示，其中0是靜音的，100是最大磁碟區。
