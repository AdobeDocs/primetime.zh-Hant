---
title: 安裝Tomcat
description: 安裝Tomcat
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# 安裝Tomcat {#install-tomcat}

您必須在兩台伺服器上安裝Tomcat。
1. 從安裝DVD的 [!DNL \Third Party\Tomcat\6.0.18\] 目錄安裝Tomcat。

   >[!NOTE]
   >
   >確保Tomcat安裝在路徑中沒有空格的位置。 您可以輸入`C:\Program Files\Tomcat`，但不能輸入`C:\Tomcat\`。

1. 要啟動Tomcat，請輸入`TomcatInstallDir>\bin\catalina.bat run`。
1. 要驗證安裝，請輸入`https://<Hostname>:8080/`以轉至Tomcat登錄頁。
1. 建立`crossdomain.xml`檔案，並將檔案放在`<TomcatInstallDir>\webapps\ROOT\`目錄中。

   您也可以從`https://drmtest2.adobe.com/crossdomain.xml`目錄複製檔案。
