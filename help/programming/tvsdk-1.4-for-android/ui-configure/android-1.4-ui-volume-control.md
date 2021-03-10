---
description: 您可以設定音量的使用者介面控制項。
title: 提供音量控制
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---


# 提供卷控制{#provide-volume-control}

您可以設定音量的使用者介面控制項。

1. 等待MediaPlayer實例處於此命令的有效狀態，該命令除RELEASED或ERROR之外。
1. 在`MediaPlayer`實例上調用`setVolume`以設定音頻音量。

   ```java
   void setVolume(int volume) throws IllegalStateException;
   ```

   卷的值表示請求的卷佔最大卷的比例，其中0為靜默，100為最大卷。

