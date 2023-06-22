---
title: 部署BEES參考實作
description: 部署BEES參考實作
copied-description: true
exl-id: 87f3f879-66b4-4b8c-a0c4-e15551f9b727
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 0%

---

# 部署BEES參考實作 {#deploy-the-bees-reference-implementation}

1. 設定您的Tomcat應用程式伺服器。 （請參閱您的Tomcat檔案）。
1. 複製 `[!DNL bees.war]` 檔案放入Tomcat的 [!DNL webapps/] 資料夾。
1. 傳送要求至 `https://localhost:8080/bees`.

   如果您看到「BEES運作中」訊息，表示部署已成功完成。
1. 在您的伺服器上啟用SSL。
