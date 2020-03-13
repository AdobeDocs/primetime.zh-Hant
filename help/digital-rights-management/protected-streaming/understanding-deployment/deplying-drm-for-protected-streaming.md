---
seo-title: 部署Adobe Primetime DRM Server以進行受保護的串流
title: 部署Adobe Primetime DRM Server以進行受保護的串流
uuid: 83ef8237-0026-4677-b42b-ea4b6de19630
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 部署Adobe Primetime DRM Server以進行受保護的串流{#deploying-the-adobe-primetime-drm-server-for-protected-streaming}

在部署Adobe Primetime DRM Server for Protected Streaming之前，您必須已安裝Java和Tomcat的版本，如「需求」主題所列。

Primetime DRM Server for Protected Streaming套件包括 [!DNL flashaccesserver.war]。 如果您：

* 要部署此WAR檔案，需要將其複製到Tomcat的目 [!DNL webapps] 錄。
* 先前已部署WAR檔案，您可能需要刪除未打包的WAR目 [!DNL flashaccessserver] 錄(在Tomcat的目 [!DNL webapps] 錄中)。

* 要防止Tomcat解壓WAR檔案，請編輯Tomcat [!DNL server.xml] 目錄中的文 [!DNL conf] 件，並通過 `unpackWARs` 將其設定為來配置該屬性 `false`。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>如果已將Tomcat配置為將 [!DNL commons-logging.jar] Tomcat包含在系統類路徑中（Primetime DRM Server for Protected Streaming不是必需的），則必須配置commons-logging以使用Log4J。

伺服器可選擇使用特定平台的程式庫( [!DNL jsafe.dll] 在Microsoft Windows或 [!DNL libjsafe.so] Linux上)，以取得最佳效能。 您可以將適合您平台的程式庫 [!DNL thirdparty/cryptoj/]*從平台&#x200B;*，複製到環境變數所指定`PATH`或Linux上`LD_LIBRARY_PATH`的位置。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>只有在作業系統和JDK都支援64位時，才應使用64位版本。 否則，您必須使用32位元版本。

