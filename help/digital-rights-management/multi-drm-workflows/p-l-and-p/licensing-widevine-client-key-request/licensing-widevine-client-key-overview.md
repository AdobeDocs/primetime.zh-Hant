---
description: 若要播放內容封裝所產生的DASH內容，TVSDK使用者端必須取得內容解密金鑰，此金鑰是在金鑰取得工作流程的封裝程式期間傳遞。 使用者端內容解密金鑰通常會由Widevine/PlayReady授權伺服器傳送給使用者端，以回應使用者端的一或多個HTTP/HTTPS貼文。
title: 使用者端金鑰請求工作流程總覽
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# 使用者端金鑰要求工作流程 {#client-key-request-workflow-overview}

若要播放內容封裝所產生的DASH內容，TVSDK使用者端必須取得內容解密金鑰，此金鑰是在金鑰取得工作流程的封裝程式期間傳遞。 使用者端內容解密金鑰通常會由Widevine/PlayReady授權伺服器傳送給使用者端，以回應使用者端的一或多個HTTP/HTTPS貼文。

若要取得內容解密金鑰，PSDK使用者端必須執行下列動作

* 抓取內容的pssh方塊，將其提供給平台，並取得金鑰要求回應。
* 透過HTTPPOST將金鑰要求傳送至適當的Widevine/PlayReady授權伺服器。
* 將伺服器的回應傳遞至平台，平台會從回應中擷取使用者端內容解密金鑰，並使用它進行內容解密。

若要針對金鑰要求傳送HTTPPOST，您的程式碼必須將授權伺服器URL以及任何需要附加至貼文的額外資料傳遞給PSDK使用者端。 要傳遞的URL和資料選擇取決於您所合作的Widevine/PlayReady服務提供者。 例如，如果您使用ExpressPlay提供服務，請傳入適當的ExpressPlay Widevine/PlayReady授權伺服器URL，並將與內容加密金鑰相關聯的ExpressPlay權杖附加至連出金鑰要求。 您可以從ExpressPlay檔案取得適當的ExpressPlay Widevine/PlayReady授權伺服器URL。
