---
title: 部署Adobe PrimetimeDRM伺服器以進行受保護的流處理
description: 部署Adobe PrimetimeDRM伺服器以進行受保護的流處理
copied-description: true
exl-id: 814c08e6-5d09-495b-b529-cedc9b9c02a7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# 部署Adobe PrimetimeDRM伺服器以進行受保護的流處理{#deploying-the-adobe-primetime-drm-server-for-protected-streaming}

在部署用於受保護流的Adobe PrimetimeDRM伺服器之前，必須已安裝Java和Tomcat版本，如「要求」主題中所列。

用於受保護流式處理的黃金時段DRM伺服器包括 [!DNL flashaccesserver.war]。 如果您：

* 要部署此WAR檔案，需要將其複製到Tomcat [!DNL webapps] 的子菜單。
* 以前已部署了WAR檔案，可能需要刪除未打包的WAR目錄( [!DNL flashaccessserver] 在Tomcat中 [!DNL webapps] )。

* 要阻止Tomcat解包WAR檔案，請編輯 [!DNL server.xml] Tomcat中的檔案 [!DNL conf] 目錄和配置 `unpackWARs` 屬性i通過將其設定為 `false`。

>[!NOTE]
>
>如果已將Tomcat配置為包括 [!DNL commons-logging.jar] 在系統類路徑（Mogfire DRM Server for Protected Streaming不是必需的）上，必須配置commons-logging以使用Log4J。

伺服器可選地使用特定於平台的庫( [!DNL jsafe.dll] 在MicrosoftWindows或 [!DNL libjsafe.so] 在Linux上實現最佳效能。 您可以從中複製適合您的平台的庫 [!DNL thirdparty/cryptoj/]*平台* 到由 `PATH` 環境變數或 `LD_LIBRARY_PATH` 在Linux上。

>[!NOTE]
>
>只有在作業系統和JDK都支援64位時，才應使用64位版本。 否則，您需要使用32位版本。
