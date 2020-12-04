---
seo-title: 部署Adobe Primetime DRM Server以進行受保護的串流
title: 部署Adobe Primetime DRM Server以進行受保護的串流
uuid: 83ef8237-0026-4677-b42b-ea4b6de19630
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# 部署Adobe Primetime DRM Server for Protected Streaming{#deploying-the-adobe-primetime-drm-server-for-protected-streaming}

在部署Adobe Primetime DRM Server for Protected Streaming之前，您必須已安裝Java和Tomcat的版本，如「需求」主題所列。

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

