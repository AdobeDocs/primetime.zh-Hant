---
seo-title: 遠端和本機iOS金鑰傳送
title: 遠端和本機iOS金鑰傳送
uuid: 90f672e7-9301-4e14-adca-db2a8f951a83
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---


# 遠程和本地iOS密鑰傳遞{#remote-and-local-ios-key-delivery}

Adobe Primetime支援下列選項，以將關鍵內容傳送至iOS用戶端：

* **Remote**  —— 如HTTP即時串流(HLS)規格中所指定執行；m3U8資訊清單指定HTTPS路徑，其中包含AES金鑰，該金鑰應用來解密串流中的下列加密區段。當您在Primetime DRM政策中指定`Remote`時，用戶端裝置必須連線至遠端HTTPS伺服器，才能取得AES金鑰。

* **本機** -當您在 `Local` Primetime DRM中指定AES金鑰，而非連線至網際網路／網路時，本機HTTPS伺服器會內嵌在iOS應用程式中，然後管理所有AES金鑰要求。內嵌的HTTPS伺服器會自動在P應用程式中設定和設定。 應用程式開發人員不需要干預。

遠端金鑰傳送是透過用於封裝內容的Primetime DRM政策來啟用。 如果您想要變更此設定，則必須重新封裝內容。 如果您啟用遠端金鑰傳送，您必須部署Primetime DRM金鑰伺服器，以管理來自iOS用戶端的金鑰要求。 不過，其他平台上的用戶端工作流程並無變更。

>[!NOTE]
>
>「金鑰傳送」選項只會影響iOS用戶端。 使用HLS內容的所有其他裝置(例如桌上型電腦上的Android和Primetime(Flash Player))，即使已指定`Remote`，也一律使用`Local`金鑰傳送。

