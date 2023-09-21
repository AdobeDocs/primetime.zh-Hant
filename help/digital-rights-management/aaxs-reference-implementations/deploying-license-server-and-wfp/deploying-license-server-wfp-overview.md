---
title: 部署授權伺服器和watched資料夾封裝程式概述
description: 部署授權伺服器和watched資料夾封裝程式概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 部署授權伺服器和watched資料夾封裝程式概述 {#deploying-the-license-server-and-watched-folder-packager-overview}

將許可證伺服器WAR檔案複製到Tomcat的 [!DNL webapps] 目錄。 如果您先前已部署WAR檔案，您可能需要手動刪除解壓縮的WAR目錄( [!DNL flashaccess]， [!DNL edcws]、和 [!DNL flashaccess-packager] 在Tomcat中 [!DNL webapps] 目錄)。 若要防止Tomcat解壓縮WAR檔案，請編輯 [!DNL server.xml] Tomcat的conf目錄中的檔案並設定 `unpackWARs` 歸因至 `false`.

屬性檔案( [!DNL flashaccess-refimpl.properties])必須在類別路徑上，伺服器才能載入屬性。 將此檔案複製到目錄，並使用適當的值更新檔案。 編輯 [!DNL catalina.properties] Tomcat中的檔案 [!DNL conf] 目錄並新增包含 [!DNL flashaccess-refimpl.properties] 至 `shared.loader` 屬性。 此 [!DNL log4j.xml] 用於設定記錄日誌的檔案也必須在類別路徑上(請參閱 [!DNL resources\log4j.xml] 例如)。

參考實作伺服器使用數個憑證檔案、原則檔案和其他資源。 這些檔案都位於一個資源資料夾中。 依預設，資源資料夾為 [!DNL C:\flashaccess-server-resources]，但此位置可在下列位置修改： [!DNL flashaccess-refimpl.properties]. 啟動伺服器之前，請務必將所有必要的資源複製到此位置。

若要啟動Tomcat和授權伺服器，請執行 `catalina.bat start` 從Tomcat&#39;s [!DNL bin] 目錄。
