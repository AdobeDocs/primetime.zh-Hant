---
seo-title: 部署WAR檔案
title: 部署WAR檔案
uuid: 435a6a6e-c981-46fb-bca9-7f5f34eecd6a
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 部署WAR檔案{#deploy-the-war-files}

1. 將WAR檔案複製到Tomcat的目 [!DNL webapps] 錄。

   * 個人化伺服器： [!DNL flashaccess.war]
   * 密鑰生成伺服器： [!DNL flashaccess-kgs.war]

1. 將資料 [!DNL ROOT] 夾從Adobe提供的套件複製到目 [!DNL webapps] 錄。

   個人化伺服器也需要主控檔 [!DNL crossdomain.xml] 案。 (檔案 [!DNL ROOT] 夾中包含 [!DNL crossdomain.xml] 檔案；必 [!DNL ROOT] 須是大寫。)密鑰生成伺服器不需要此檔案。

