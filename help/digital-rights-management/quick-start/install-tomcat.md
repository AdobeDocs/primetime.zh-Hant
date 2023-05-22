---
title: 安裝Tomcat
description: 安裝Tomcat
copied-description: true
exl-id: aed8fc1c-0d75-47ca-bbd4-c0934a66e284
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# 安裝Tomcat {#install-tomcat}

必須在兩台伺服器上安裝Tomcat。
1. 從 [!DNL \Third Party\Tomcat\6.0.18\] 目錄中的x_ server程式。

   >[!NOTE]
   >
   >確保在路徑中沒有空格的位置安裝了Tomcat。 您可以輸入 `C:\Program Files\Tomcat`，但 `C:\Tomcat\`。

1. 要啟動Tomcat，請輸入 `TomcatInstallDir>\bin\catalina.bat run`。
1. 要驗證安裝，請通過輸入 `https://<Hostname>:8080/`。
1. 建立 `crossdomain.xml` 並將檔案放在 `<TomcatInstallDir>\webapps\ROOT\` 的子菜單。

   也可以從 `https://drmtest2.adobe.com/crossdomain.xml` 的子菜單。
