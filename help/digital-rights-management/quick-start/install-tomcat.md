---
title: 安裝Tomcat
description: 安裝Tomcat
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# 安裝Tomcat {#install-tomcat}

您必須在兩部伺服器上安裝Tomcat。
1. 從安裝Tomcat [!DNL \Third Party\Tomcat\6.0.18\] 目錄。

   >[!NOTE]
   >
   >請確定Tomcat安裝在路徑中沒有空格的位置。 您可以輸入 `C:\Program Files\Tomcat`，但不提供 `C:\Tomcat\`.

1. 若要啟動Tomcat，請輸入 `TomcatInstallDir>\bin\catalina.bat run`.
1. 若要驗證安裝，請前往Tomcat登陸頁面，輸入 `https://<Hostname>:8080/`.
1. 建立 `crossdomain.xml` 檔案並將檔案置於 `<TomcatInstallDir>\webapps\ROOT\` 目錄。

   您也可以從以下位置複製檔案： `https://drmtest2.adobe.com/crossdomain.xml` 目錄。
