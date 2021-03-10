---
title: 部署WAR檔案
description: 部署WAR檔案
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 0%

---


# 部署WAR檔案{#deploy-the-war-files}

1. 將WAR檔案複製到Tomcat的[!DNL webapps]目錄。

   * 個人化伺服器：[!DNL flashaccess.war]
   * 密鑰生成伺服器：[!DNL flashaccess-kgs.war]

1. 將[!DNL ROOT]資料夾從Adobe提供的包複製到[!DNL webapps]目錄。

   個人化伺服器還需要托管[!DNL crossdomain.xml]檔案。 ([!DNL ROOT]資料夾包含[!DNL crossdomain.xml]檔案；[!DNL ROOT]必須為所有大寫。) 密鑰生成伺服器不需要此檔案。

