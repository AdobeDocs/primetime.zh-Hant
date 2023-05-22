---
description: 您可以通過建立備用音頻功能管理器將延遲綁定或備用音頻流整合到播放器中。
title: 整合後綁定音頻
exl-id: 43be9042-d547-4646-a920-cdd2a5dbb1fb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---

# 整合後綁定音頻 {#integrate-late-binding-audio}

您可以通過建立備用音頻功能管理器將延遲綁定或備用音頻流整合到播放器中。

* 要建立備用音頻管理器：

   ```java
   AAManager aaManager = new AAManagerOn(); 
   ```

* 要使用ManagerFactory啟用備用音頻，請確保以下代碼行位於 `PlayerFragment.java` 檔案：

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>true</b>,config, mediaPlayer);
   ```

   禁用備用音頻：

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>false</b>,config, mediaPlayer);
   ```
