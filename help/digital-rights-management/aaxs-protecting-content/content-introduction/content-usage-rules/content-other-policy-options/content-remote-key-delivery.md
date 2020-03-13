---
seo-title: 遠端和本機iOS金鑰傳送
title: 遠端和本機iOS金鑰傳送
uuid: 3c20b1d1-f842-438a-ae3a-4ec31da306ad
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 遠端和本機iOS金鑰傳送{#remote-and-local-ios-key-delivery}

Adobe Primetime支援兩種選項，可將關鍵內容傳送至iOS用戶端：

* 遠端- M3U8資訊清單正如HLS規格中所指定，指定包含AES金鑰的HTTPS路徑，該金鑰應用來解密串流中的下列加密區段。 指定&quot;Remote&quot;時，客戶端設備將連接到遠程HTTPS伺服器以獲取AES密鑰。
* 本地——指定「本地」時，本地HTTPS伺服器將嵌入iOS應用程式中，該應用程式將處理所有AES密鑰請求，而不是通過Internet/網路訪問AES密鑰。 內嵌的HTTPS伺服器會自動在Primetime應用程式中設定和設定。 應用程式開發人員不需要干預。

遠端金鑰傳送是透過用來封裝內容的原則來啟用（變更此設定需要重新封裝內容）。啟用遠端金鑰傳送時，必須部署Adobe Access Key Server來處理來自iOS用戶端的金鑰要求，但是其他平台上的用戶端工作流程並未變更。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>「金鑰傳送」選項只會影響iOS用戶端。 使用HLS內容的所有其他設備始終使用「本地」密鑰傳遞，即使已指定「遠程」。

如需詳細資訊，請 *參閱「使用Adobe Access Key Server*」。
