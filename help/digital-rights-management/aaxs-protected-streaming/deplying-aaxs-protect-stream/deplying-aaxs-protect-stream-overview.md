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


# 部署Adobe Access Server for Protected Streaming概觀 {#deploying-the-adobe-access-server-for-protected-streaming-overview}

在部署Adobe Access Server for Protected Streaming之前，請確定您已安裝「需求」區段中所列的Java和Tomcat版本。

Adobe Access Server for Protected Streaming套件包含在內 [!DNL flashaccesserver.war]。 要部署此WAR檔案，請將其複製到Tomcat的目 [!DNL webapps] 錄。 如果先前已部署WAR檔案，則可能需要手動刪除未打包的WAR目 [!DNL flashaccessserver] 錄(在Tomcat的目 [!DNL webapps] 錄中)。 為防止Tomcat解壓縮WAR檔案，請編 [!DNL server.xml] 輯Tomcat目錄中的 [!DNL conf] 檔案，並將屬 `unpackWARs` 性設定為 `false`。

>[!NOTE]
>
>如果已將Tomcat配置為 [!DNL commons-logging.jar] 在系統類路徑中包括（Adobe Access Server for Protected Streaming不是必需的），則必須將commons-logging配置為使用Log4J。

伺服器可選擇使用特定平台的程式庫( [!DNL jsafe.dll] 在Microsoft Windows或 [!DNL libjsafe.so] 在Linux上)，以提供最佳效能。 將適合您平台的程式庫 [!DNL thirdparty/cryptoj/]*從平台&#x200B;*，複製至環境變數(或`PATH``LD_LIBRARY_PATH`在Linux上)所指定的位置。

>[!NOTE]
>
>64位元版本僅在作業系統和JDK都支援64位元時使用，否則應使用32位元版本。

