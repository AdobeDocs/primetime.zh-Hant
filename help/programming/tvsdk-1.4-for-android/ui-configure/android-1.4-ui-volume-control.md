---
description: 可以設定聲音音量的用戶介面控制項。
title: 提供音量控制
exl-id: aa8ffdf3-515b-4899-8a00-8fb5b8c595a9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---

# 提供音量控制{#provide-volume-control}

可以設定聲音音量的用戶介面控制項。

1. 等待MediaPlayer實例處於此命令的有效狀態，該命令除RELEASED或ERROR外。
1. 呼叫 `setVolume` 的 `MediaPlayer` 實例，以設定音頻卷。

   ```java
   void setVolume(int volume) throws IllegalStateException;
   ```

   卷的值表示請求的卷佔最大卷的比例，其中0為靜默，100為最大卷。
