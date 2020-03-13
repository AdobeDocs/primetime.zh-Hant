---
description: 若要播放內容封裝產生的DASH內容，TVSDK用戶端將需要取得在封裝程式期間在擷取關鍵字工作流程中傳遞的內容解密金鑰。 客戶端內容解密密鑰通常由Widevine/PlayReady許可伺服器響應於來自客戶端的一個或多個HTTP/HTTPS帖子而傳遞給客戶端。
seo-description: 若要播放內容封裝產生的DASH內容，TVSDK用戶端將需要取得在封裝程式期間在擷取關鍵字工作流程中傳遞的內容解密金鑰。 客戶端內容解密密鑰通常由Widevine/PlayReady許可伺服器響應於來自客戶端的一個或多個HTTP/HTTPS帖子而傳遞給客戶端。
seo-title: 用戶端金鑰要求工作流程總覽
title: 用戶端金鑰要求工作流程總覽
uuid: 2f01f0ae-adbf-42fa-a908-4b5b9410a26d
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# 用戶端金鑰要求工作流程 {#client-key-request-workflow-overview}

若要播放內容封裝產生的DASH內容，TVSDK用戶端將需要取得在封裝程式期間在擷取關鍵字工作流程中傳遞的內容解密金鑰。 客戶端內容解密密鑰通常由Widevine/PlayReady許可伺服器響應於來自客戶端的一個或多個HTTP/HTTPS帖子而傳遞給客戶端。

若要取得內容解密金鑰，PSDK用戶端必須執行下列動作

* 擷取內容的pssh方塊，將它提供給平台，並取得回應金鑰要求。
* 透過HTTP POST，將金鑰要求傳送至適當的Widevine/PlayReady授權伺服器。
* 將伺服器的響應傳遞給平台，該平台將從響應中提取客戶端內容解密密鑰，並將其用於內容解密。

若要送出HTTP POST以索取關鍵要求，您的程式碼必須將授權伺服器URL以及任何需要附加至貼文的額外資料傳送至PSDK用戶端。 要傳遞的URL和資料選擇取決於您所使用的Widevine/PlayReady服務供應商。 例如，如果您使用ExpressPlay提供服務，請傳入適當的ExpressPlay Widevine/PlayReady授權伺服器URL，並附加至傳出金鑰要求中與內容加密金鑰關聯的ExpressPlay Token。 您可從ExpressPlay檔案取得適當的ExpressPlay Widevine/PlayReady授權伺服器URL。