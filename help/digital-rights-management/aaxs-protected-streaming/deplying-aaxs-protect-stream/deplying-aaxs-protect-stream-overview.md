---
title: 部署Adobe Access Server for Protected Streaming概述
description: 部署Adobe Access Server for Protected Streaming概述
copied-description: true
exl-id: fdefa13a-14ec-4301-ab39-2ceea830463d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 部署Adobe Access Server for Protected Streaming概述 {#deploying-the-adobe-access-server-for-protected-streaming-overview}

部署Adobe Access Server for Protected Streaming之前，請確定您已安裝「需求」區段中列出的Java和Tomcat版本。

適用於受保護串流套件的Adobe Access Server包含 [!DNL flashaccesserver.war]. 若要部署此WAR檔案，請將其複製到Tomcat的 [!DNL webapps] 目錄。 如果您先前已部署WAR檔案，您可能需要手動刪除解壓縮的WAR目錄( [!DNL flashaccessserver] 在Tomcat的 [!DNL webapps] 目錄)。 若要防止Tomcat解壓縮WAR檔案，請編輯 [!DNL server.xml] tomcat中的檔案 [!DNL conf] 目錄並設定 `unpackWARs` 屬性至 `false`.

>[!NOTE]
>
>如果您已將Tomcat設定為包含 [!DNL commons-logging.jar] 在系統類別路徑(Protected Streaming不需要Adobe Access Server)上，commons-logging必須設定為使用Log4J。

伺服器可選擇使用平台專屬的程式庫( [!DNL jsafe.dll] 在Microsoft Windows上或 [!DNL libjsafe.so] （在Linux上）以獲得最佳效能。 從以下位置複製適合您平台的資料庫： [!DNL thirdparty/cryptoj/]*平台* 至指定的位置 `PATH` 環境變數(或 `LD_LIBRARY_PATH` （在Linux上）。

>[!NOTE]
>
>64位元版本只有在作業系統和JDK都支援64位元時才應該使用，否則請使用32位元版本。
