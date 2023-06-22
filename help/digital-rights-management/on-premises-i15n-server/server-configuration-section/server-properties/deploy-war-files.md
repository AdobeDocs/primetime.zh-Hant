---
title: 部署WAR檔案
description: 部署WAR檔案
copied-description: true
exl-id: 9f491596-2a02-4a55-9baa-86407e389d20
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 0%

---

# 部署WAR檔案{#deploy-the-war-files}

1. 將WAR檔案複製到Tomcat的 [!DNL webapps] 目錄。

   * 個人化伺服器： [!DNL flashaccess.war]
   * 金鑰產生伺服器： [!DNL flashaccess-kgs.war]

1. 複製 [!DNL ROOT] 資料夾(從Adobe提供的套件中至 [!DNL webapps] 目錄。

   個人化伺服器也需要託管 [!DNL crossdomain.xml] 檔案。 (此 [!DNL ROOT] 資料夾包含 [!DNL crossdomain.xml] 檔案； [!DNL ROOT] 必須全部大寫。) 金鑰產生伺服器不需要此檔案。
