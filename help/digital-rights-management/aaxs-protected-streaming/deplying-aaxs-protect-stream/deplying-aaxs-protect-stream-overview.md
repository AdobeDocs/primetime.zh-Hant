---
title: 部署Adobe Access Server for Protected Streaming概述
description: 部署Adobe Access Server for Protected Streaming概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 部署Adobe Access Server for Protected Streaming概述 {#deploying-the-adobe-access-server-for-protected-streaming-overview}

在部署Adobe Access Server for Protected Streaming之前，請確定您已安裝「需求」區段中列出的Java和Tomcat版本。

適用於受保護串流的Adobe Access Server套件包括 [!DNL flashaccesserver.war]. 若要部署此WAR檔案，請將其複製到Tomcat的 [!DNL webapps] 目錄。 如果您先前已部署WAR檔案，您可能需要手動刪除解壓縮的WAR目錄( [!DNL flashaccessserver] 在Tomcat中 [!DNL webapps] 目錄)。 若要防止Tomcat解壓縮WAR檔案，請編輯 [!DNL server.xml] Tomcat中的檔案 [!DNL conf] 目錄並設定 `unpackWARs` 歸因至 `false`.

>[!NOTE]
>
>如果您已將Tomcat設定為包含 [!DNL commons-logging.jar] 在系統類別路徑(Protected Streaming不需要Adobe Access Server)上，commons-logging必須設定為使用Log4J。

伺服器可選擇使用平台專屬的程式庫( [!DNL jsafe.dll] 在Microsoft Windows上或 [!DNL libjsafe.so] （在Linux上）以獲得最佳效能。 從複製您平台的適當程式庫 [!DNL thirdparty/cryptoj/]*平台* 至指定的位置 `PATH` 環境變數(或 `LD_LIBRARY_PATH` 在Linux上)。

>[!NOTE]
>
>只有在作業系統和JDK都支援64位元時，才應該使用64位元版本，否則請使用32位元版本。
