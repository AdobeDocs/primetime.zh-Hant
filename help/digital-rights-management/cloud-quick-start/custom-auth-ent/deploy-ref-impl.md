---
title: 部署BEES參考實施
description: 部署BEES參考實施
copied-description: true
exl-id: 87f3f879-66b4-4b8c-a0c4-e15551f9b727
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 0%

---

# 部署BEES參考實施 {#deploy-the-bees-reference-implementation}

1. 設定Tomcat應用程式伺服器。 （請參閱Tomcat文檔。）
1. 複製 `[!DNL bees.war]` 檔案到Tomcat [!DNL webapps/] 的子菜單。
1. 將請求發送到 `https://localhost:8080/bees`。

   如果您看到「蜂類正在操作」消息，則部署已成功完成。
1. 在伺服器上啟用SSL。
