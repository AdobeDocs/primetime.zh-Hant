---
title: 部署授權伺服器和受監視的資料夾封裝程式總覽
description: 部署授權伺服器和受監視的資料夾封裝程式總覽
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# 部署許可證伺服器和監視資料夾包器概述{#deploying-the-license-server-and-watched-folder-packager-overview}

將許可證伺服器WAR檔案複製到Tomcat的[!DNL webapps]目錄。 如果先前已部署了WAR檔案，則可能需要手動刪除Tomcat的[!DNL webapps]目錄中未打包的WAR目錄（[!DNL flashaccess]、[!DNL edcws]和[!DNL flashaccess-packager]）。 為防止Tomcat解壓WAR檔案，請編輯Tomcat的conf目錄中的[!DNL server.xml]檔案，並將`unpackWARs`屬性設定為`false`。

屬性檔案([!DNL flashaccess-refimpl.properties])必須位於類路徑中，伺服器才能載入屬性。 將此檔案複製到目錄，並使用適當的值更新檔案。 編輯Tomcat的[!DNL conf]目錄中的[!DNL catalina.properties]檔案，並將包含[!DNL flashaccess-refimpl.properties]的目錄添加到`shared.loader`屬性中。 用於配置日誌記錄的[!DNL log4j.xml]檔案也必須位於類路徑中（例如，請參見[!DNL resources\log4j.xml]）。

參考實施伺服器使用多個證書檔案、策略檔案和其他資源。 這些檔案都位於一個資源資料夾中。 預設情況下，資源資料夾為[!DNL C:\flashaccess-server-resources]，但可以在[!DNL flashaccess-refimpl.properties]中修改此位置。 在啟動伺服器之前，請務必將所有必需資源複製到此位置。

要啟動Tomcat和許可證伺服器，請從Tomcat的[!DNL bin]目錄運行`catalina.bat start`。
