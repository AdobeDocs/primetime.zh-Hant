---
seo-title: 部署Adobe Access Server for Protected Streaming概觀
title: 部署Adobe Access Server for Protected Streaming概觀
uuid: 48a7e452-520a-4ff8-97e9-11210221256d
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# 部署Adobe Access Server for Protected Streaming概觀{#deploying-the-adobe-access-server-for-protected-streaming-overview}

在部署Adobe Access Server for Protected Streaming之前，請確定您已安裝「需求」區段中所列的Java和Tomcat版本。

Adobe Access Server for Protected Streaming套件包含[!DNL flashaccesserver.war]。 要部署此WAR檔案，請將其複製到Tomcat的[!DNL webapps]目錄。 如果先前已部署WAR檔案，則可能需要手動刪除未打包的WAR目錄（Tomcat的[!DNL webapps]目錄中的[!DNL flashaccessserver]）。 為防止Tomcat解壓WAR檔案，請編輯Tomcat的[!DNL conf]目錄中的[!DNL server.xml]檔案，並將`unpackWARs`屬性設定為`false`。

>[!NOTE]
>
>如果已將Tomcat配置為在系統類路徑中包含[!DNL commons-logging.jar]（對於受保護流的Adobe Access Server不是必需的），則必須將commons-logging配置為使用Log4J。

伺服器可選地使用特定平台的庫（在Microsoft Windows上為[!DNL jsafe.dll]或在Linux上為[!DNL libjsafe.so]）來獲得最佳效能。 將適合您平台的程式庫從&#x200B;[!DNL thirdparty/cryptoj/]*platform*&#x200B;複製至`PATH`環境變數（或`LD_LIBRARY_PATH` on Linux）所指定的位置。

>[!NOTE]
>
>64位元版本僅在作業系統和JDK都支援64位元時使用，否則應使用32位元版本。

