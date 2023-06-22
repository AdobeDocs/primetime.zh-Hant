---
description: 您可以建立替代音訊功能管理員，將後期繫結或替代音訊串流整合到播放器中。
title: 整合後期繫結音訊
exl-id: 43be9042-d547-4646-a920-cdd2a5dbb1fb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---

# 整合後期繫結音訊 {#integrate-late-binding-audio}

您可以建立替代音訊功能管理員，將後期繫結或替代音訊串流整合到播放器中。

* 若要建立替代的音訊管理員：

   ```java
   AAManager aaManager = new AAManagerOn(); 
   ```

* 若要使用ManagerFactory來啟用替代音訊，請確定下列程式碼行位於 `PlayerFragment.java` 檔案：

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>true</b>,config, mediaPlayer);
   ```

   停用替代音訊：

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>false</b>,config, mediaPlayer);
   ```
