---
description: 您可以建立替代音訊功能管理員，將後期繫結或替代音訊串流整合至播放器。
title: 整合後期繫結音訊
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---

# 整合後期繫結音訊 {#integrate-late-binding-audio}

您可以建立替代音訊功能管理員，將後期繫結或替代音訊串流整合至播放器。

* 若要建立替代音訊管理員：

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
