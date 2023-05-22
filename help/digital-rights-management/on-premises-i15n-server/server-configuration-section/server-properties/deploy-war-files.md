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

1. 將WAR檔案複製到Tomcat [!DNL webapps] 的子菜單。

   * 個性化伺服器： [!DNL flashaccess.war]
   * 密鑰生成伺服器： [!DNL flashaccess-kgs.war]

1. 複製 [!DNL ROOT] 資料夾從Adobe提供的包到 [!DNL webapps] 的子菜單。

   個性化伺服器還需要承載 [!DNL crossdomain.xml] 的子菜單。 ( [!DNL ROOT] 資料夾包含 [!DNL crossdomain.xml] 檔案； [!DNL ROOT] 必須是大寫。) 密鑰生成伺服器不需要此檔案。
