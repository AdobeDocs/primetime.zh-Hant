---
description: 您可以建立替代的音訊功能管理員，將延遲系結或替代的音訊串流整合至您的播放器。
title: 整合後期系結音訊
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# 整合後期系結音訊{#integrate-late-binding-audio}

您可以建立替代的音訊功能管理員，將延遲系結或替代的音訊串流整合至您的播放器。

* 要建立備用音頻管理器，請執行以下操作：

   ```java
   AAManager aaManager = new AAManagerOn(); 
   ```

* 要使用ManagerFactory啟用備用音頻，請確保`PlayerFragment.java`檔案中包含以下代碼行：

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>true</b>,config, mediaPlayer);
   ```

   要禁用備用音頻，請執行以下操作：

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>false</b>,config, mediaPlayer);
   ```

