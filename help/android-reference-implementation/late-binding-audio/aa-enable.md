---
description: 您可以建立替代的音訊功能管理員，將延遲系結或替代的音訊串流整合至您的播放器。
seo-description: 您可以建立替代的音訊功能管理員，將延遲系結或替代的音訊串流整合至您的播放器。
seo-title: 整合後期系結音訊
title: 整合後期系結音訊
uuid: cd2e259a-2af4-4d7b-a856-79bd087e8ca6
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 整合後期系結音訊 {#integrate-late-binding-audio}

您可以建立替代的音訊功能管理員，將延遲系結或替代的音訊串流整合至您的播放器。

* 要建立備用音頻管理器，請執行以下操作：

   ```java
   AAManager aaManager = new AAManagerOn(); 
   ```

* 要使用ManagerFactory啟用備用音頻，請確保檔案中包含以下代碼 `PlayerFragment.java` 行：

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>true</b>,config, mediaPlayer);
   ```

   要禁用備用音頻，請執行以下操作：

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>false</b>,config, mediaPlayer);
   ```

