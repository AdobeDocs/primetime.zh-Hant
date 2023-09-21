---
title: 為受保護的串流部署Adobe Primetime DRM伺服器
description: 為受保護的串流部署Adobe Primetime DRM伺服器
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# 為受保護的串流部署Adobe Primetime DRM伺服器{#deploying-the-adobe-primetime-drm-server-for-protected-streaming}

您必須先安裝「需求」主題中所列的Java和Tomcat版本，才能部署Adobe Primetime DRM Server for Protected Streaming。

Primetime DRM Server for Protected Streaming套件包括 [!DNL flashaccesserver.war]. 如果您：

* 若要部署此WAR檔案，您必須將其複製到Tomcat的 [!DNL webapps] 目錄。
* 先前已部署WAR檔案，您可能需要刪除解壓縮的WAR目錄( [!DNL flashaccessserver] 在Tomcat中 [!DNL webapps] 目錄)。

* 要防止Tomcat解壓縮WAR檔案，請編輯 [!DNL server.xml] Tomcat中的檔案 [!DNL conf] 目錄並設定 `unpackWARs` 屬性，方法是將其設定為 `false`.

>[!NOTE]
>
>如果您已將Tomcat設定為包含 [!DNL commons-logging.jar] 在「系統」類別路徑（Primetime DRM Server for Protected Streaming不需要）上，您必須設定commons-logging以使用Log4J。

伺服器可選擇使用平台專屬的程式庫( [!DNL jsafe.dll] 在Microsoft Windows上或 [!DNL libjsafe.so] 在Linux上以獲得最佳效能。 您可以從以下位置複製適合您平台的資料庫： [!DNL thirdparty/cryptoj/]*平台* 至指定的位置 `PATH` 環境變數或 `LD_LIBRARY_PATH` 在Linux上。

>[!NOTE]
>
>如果作業系統和JDK都支援64位元，您應該只使用64位元版本。 否則，您需要使用32位元版本。
