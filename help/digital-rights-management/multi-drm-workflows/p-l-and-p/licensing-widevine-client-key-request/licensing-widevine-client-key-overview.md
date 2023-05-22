---
description: 若要播放內容打包產生的DASH內容，TVSDK客戶端需要獲取在打包過程中在密鑰獲取工作流中傳遞的內容解密密鑰。 客戶端內容解密密鑰通常由Widevine/PlayReady許可證伺服器響應於來自客戶端的一個或多個HTTP/HTTPS帖子而傳送到客戶端。
title: 客戶端密鑰請求工作流概述
exl-id: ae600cbd-415b-441a-bf01-f259993071f2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# 客戶端密鑰請求工作流 {#client-key-request-workflow-overview}

若要播放內容打包產生的DASH內容，TVSDK客戶端需要獲取在打包過程中在密鑰獲取工作流中傳遞的內容解密密鑰。 客戶端內容解密密鑰通常由Widevine/PlayReady許可證伺服器響應於來自客戶端的一個或多個HTTP/HTTPS帖子而傳送到客戶端。

要獲取內容解密密鑰，PSDK客戶端必須執行以下操作

* 抓住內容的pssh框，將其提供給平台，並獲取響應密鑰請求。
* 通過HTTPPOST將密鑰請求發送到相應的Widevine/PlayReady許可證伺服器。
* 將伺服器的響應傳遞給平台，該平台將從響應中提取客戶端內容解密密鑰並將其用於內容解密。

要發送密鑰請求的HTTPPOST，您的代碼必須將許可證伺服器URL連同需要附加到帖子的任何額外資料傳遞給PSDK客戶端。 要傳遞的URL和資料的選擇取決於您所使用的Widevine/PlayReady服務提供商。 例如，如果使用ExpressPlay提供服務，則您將傳遞相應的ExpressPlay Widevine/PlayReady許可證伺服器URL，並將與內容的加密密鑰關聯的ExpressPlay令牌附加到傳出密鑰請求。 可以從ExpressPlay文檔獲取相應的ExpressPlay Widevine/PlayReady許可證伺服器URL。
