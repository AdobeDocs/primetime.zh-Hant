---
title: 部署Adobe PrimetimeDRM Server進行受保護的串流
description: 部署Adobe PrimetimeDRM Server進行受保護的串流
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# 部署Adobe PrimetimeDRM Server for Protected Streaming{#deploying-the-adobe-primetime-drm-server-for-protected-streaming}

在部署用於受保護流的Adobe PrimetimeDRM伺服器之前，必須已安裝Java和Tomcat的版本，如「要求」主題中所列。

Primetime DRM Server for Protected Streaming套件包含[!DNL flashaccesserver.war]。 如果您：

* 要部署此WAR檔案，需要將其複製到Tomcat的[!DNL webapps]目錄。
* 先前已部署WAR檔案，您可能需要刪除未打包的WAR目錄（Tomcat的[!DNL webapps]目錄中的[!DNL flashaccessserver]）。

* 要防止Tomcat解壓縮WAR檔案，請編輯Tomcat的[!DNL conf]目錄中的[!DNL server.xml]檔案，並通過將其設定為`false`來配置`unpackWARs`屬性。

>[!NOTE]
>
>如果已將Tomcat配置為在系統類路徑中包含[!DNL commons-logging.jar]（Primetime DRM Server for Protected Streaming不是必需的），則必須配置commons-logging以使用Log4J。

伺服器可選地使用特定於平台的庫(在Microsoft Windows上為[!DNL jsafe.dll] ，在Linux上為[!DNL libjsafe.so] ，以獲得最佳效能。 您可以從&#x200B;[!DNL thirdparty/cryptoj/]*platform*&#x200B;將適合您平台的程式庫複製到`PATH`環境變數或`LD_LIBRARY_PATH`在Linux上指定的位置。

>[!NOTE]
>
>只有在作業系統和JDK都支援64位時，才應使用64位版本。 否則，您必須使用32位元版本。

