---
title: 部署Adobe Primetime DRM Server for Protected Streaming
description: 部署Adobe Primetime DRM Server for Protected Streaming
copied-description: true
exl-id: 814c08e6-5d09-495b-b529-cedc9b9c02a7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# 部署Adobe Primetime DRM Server for Protected Streaming{#deploying-the-adobe-primetime-drm-server-for-protected-streaming}

您必須先安裝「需求」主題中所列的Java和Tomcat版本，才能部署Adobe Primetime DRM Server for Protected Streaming。

Primetime DRM Server for Protected Streaming套件包含 [!DNL flashaccesserver.war]. 如果您：

* 若要部署此WAR檔案，您必須將其複製到Tomcat的 [!DNL webapps] 目錄。
* 先前已部署WAR檔案，您可能需要刪除解壓縮的WAR目錄( [!DNL flashaccessserver] 在Tomcat的 [!DNL webapps] 目錄)。

* 若要防止Tomcat解壓縮WAR檔案，請編輯 [!DNL server.xml] tomcat中的檔案 [!DNL conf] 目錄並設定 `unpackWARs` 屬性（透過將其設定為） `false`.

>[!NOTE]
>
>如果您已將Tomcat設定為包含 [!DNL commons-logging.jar] 在系統類別路徑上（Primetime DRM伺服器不需要Protected Streaming），您必須設定commons-logging才能使用Log4J。

伺服器可選擇使用平台專屬的程式庫( [!DNL jsafe.dll] 在Microsoft Windows上或 [!DNL libjsafe.so] 在Linux上以取得最佳效能。 您可以從以下位置複製適合您平台的程式庫： [!DNL thirdparty/cryptoj/]*平台* 至指定的位置 `PATH` 環境變數或 `LD_LIBRARY_PATH` 在Linux上。

>[!NOTE]
>
>如果作業系統和JDK都支援64位元，您應該只使用64位元版本。 否則，您需要使用32位元版本。
