---
title: 部署許可證伺服器和受監視資料夾打包程式概述
description: 部署許可證伺服器和受監視資料夾打包程式概述
copied-description: true
exl-id: b44aec8b-f1d7-4dce-bc51-0ce2b74ae0c1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 部署許可證伺服器和受監視資料夾打包程式概述 {#deploying-the-license-server-and-watched-folder-packager-overview}

將許可證伺服器WAR檔案複製到Tomcat [!DNL webapps] 的子菜單。 如果以前部署過WAR檔案，則可能需要手動刪除未打包的WAR目錄( [!DNL flashaccess]。 [!DNL edcws], [!DNL flashaccess-packager] 在Tomcat中 [!DNL webapps] )。 要防止Tomcat解包WAR檔案，請編輯 [!DNL server.xml] 檔案，並設定 `unpackWARs` 屬性 `false`。

屬性檔案( [!DNL flashaccess-refimpl.properties])必須位於類路徑中，伺服器才能載入屬性。 將此檔案複製到目錄，並使用相應的值更新檔案。 編輯 [!DNL catalina.properties] Tomcat中的檔案 [!DNL conf] 目錄並添加包含 [!DNL flashaccess-refimpl.properties] 到 `shared.loader` 屬性。 的 [!DNL log4j.xml] 用於配置日誌記錄的檔案也必須位於類路徑中（請參見） [!DNL resources\log4j.xml] 例如)。

參考實現伺服器使用多個證書檔案、策略檔案和其他資源。 這些檔案都位於一個資源資料夾中。 預設情況下，資源資料夾為 [!DNL C:\flashaccess-server-resources]，但可以在中修改此位置 [!DNL flashaccess-refimpl.properties]。 在啟動伺服器之前，請確保將所有所需資源複製到此位置。

要啟動Tomcat和許可證伺服器，請運行 `catalina.bat start` 從Tomcat [!DNL bin] 的子菜單。
