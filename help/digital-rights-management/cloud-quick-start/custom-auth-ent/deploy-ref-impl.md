---
title: 部署BEES參考實作
description: 部署BEES參考實作
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 0%

---


# 部署BEES參考實施{#deploy-the-bees-reference-implementation}

1. 設定Tomcat應用程式伺服器。 （請參閱Tomcat檔案。）
1. 將`[!DNL bees.war]`檔案複製到Tomcat的[!DNL webapps/]資料夾中。
1. 傳送要求至`https://localhost:8080/bees`。

   如果您看到「蜂類正在運行」消息，則部署已成功完成。
1. 在您的伺服器上啟用SSL。
