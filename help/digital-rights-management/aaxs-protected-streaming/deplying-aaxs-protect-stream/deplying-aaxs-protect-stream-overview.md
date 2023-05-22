---
title: 部署Adobe Access Server以獲得保護的流式處理概述
description: 部署Adobe Access Server以獲得保護的流式處理概述
copied-description: true
exl-id: fdefa13a-14ec-4301-ab39-2ceea830463d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 部署Adobe Access Server以獲得保護的流式處理概述 {#deploying-the-adobe-access-server-for-protected-streaming-overview}

在部署用於受保護流的Adobe Access Server之前，請確保已安裝「要求」部分中列出的Java和Tomcat版本。

Adobe Access Server的受保護流包包括 [!DNL flashaccesserver.war]。 要部署此WAR檔案，請將其複製到Tomcat [!DNL webapps] 的子菜單。 如果以前部署過WAR檔案，則可能需要手動刪除解壓縮的WAR目錄( [!DNL flashaccessserver] 在Tomcat中 [!DNL webapps] )。 要防止Tomcat解包WAR檔案，請編輯 [!DNL server.xml] Tomcat中的檔案 [!DNL conf] 目錄和設定 `unpackWARs` 屬性 `false`。

>[!NOTE]
>
>如果已將Tomcat配置為包括 [!DNL commons-logging.jar] 在系統類路徑(受保護流的Adobe Access Server不需要)上，必須將commons-logging配置為使用Log4J。

伺服器可選地使用特定於平台的庫( [!DNL jsafe.dll] 在MicrosoftWindows或 [!DNL libjsafe.so] 在Linux上)，以獲得最佳效能。 從中複製適合您的平台的庫 [!DNL thirdparty/cryptoj/]*平台* 到由 `PATH` 環境變數 `LD_LIBRARY_PATH` 在Linux上)。

>[!NOTE]
>
>只有在作業系統和JDK都支援64位時，才應使用64位版本，否則應使用32位版本。
