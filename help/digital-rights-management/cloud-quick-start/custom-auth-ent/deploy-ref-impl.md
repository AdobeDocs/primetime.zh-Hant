---
title: 部署BEES參考實作
description: 部署BEES參考實作
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 0%

---

# 部署BEES參考實作 {#deploy-the-bees-reference-implementation}

1. 設定您的Tomcat應用程式伺服器。 （請參閱您的Tomcat檔案）。
1. 複製 `[!DNL bees.war]` 檔案進入Tomcat的 [!DNL webapps/] 資料夾。
1. 傳送要求至 `https://localhost:8080/bees`.

   如果您看到「BEES運作中」訊息，表示部署已成功完成。
1. 在您的伺服器上啟用SSL。
