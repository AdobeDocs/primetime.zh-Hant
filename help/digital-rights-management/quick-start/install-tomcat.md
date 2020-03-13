---
seo-title: 安裝Tomcat
title: 安裝Tomcat
uuid: f7663eda-ad18-4a6e-bb9f-01c74721b047
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c

---


# 安裝Tomcat {#install-tomcat}

您必須在兩台伺服器上安裝Tomcat。
1. 從安裝DVD上的[!DNL \Third Party\Tomcat\6.0.18\]目錄安裝Tomcat。

   >[!NOTE]
   >
   >確保Tomcat安裝在路徑中沒有空格的位置。 您可以輸入， `C:\Program Files\Tomcat`但不能輸入 `C:\Tomcat\`。

1. 要啟動Tomcat，請輸入 `TomcatInstallDir>\bin\catalina.bat run`。
1. 要驗證安裝，請通過輸入轉到Tomcat登錄頁 `https://<Hostname>:8080/`。
1. 建立文 `crossdomain.xml` 件並將檔案放在目 `<TomcatInstallDir>\webapps\ROOT\` 錄中。

   您也可以從目錄中複製 `https://drmtest2.adobe.com/crossdomain.xml` 檔案。
