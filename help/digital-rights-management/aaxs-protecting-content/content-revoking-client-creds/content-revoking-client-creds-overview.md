---
seo-title: 廢止用戶端認證
title: 廢止用戶端認證
uuid: 47f1ec1a-bd8f-4f8c-bee3-bfbf6d9902e7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 廢止用戶端認證{#revoking-client-credentials}

在某些情況下，必須撤銷客戶端的憑據，或檢查給定的一組憑據是否已被撤銷。 如果證書受到危害，則可撤銷證書。 發生此情況時，授權將不再發給受損客戶。

Adobe會維護「憑證撤銷清單」(CRL)，以撤銷受危害的客戶。 這些CRL由SDK自動執行。 許可伺服器可以通過禁止特定電腦認證或特定版本的DRM和運行時認證進一步限制客戶端。 可 `RevocationList` 以建立並傳入SDK以廢止電腦憑證。 特定的DRM/執行時期版本可以在策略級別（通過在播放權中設定模組限制）或全局(通過在中設定模組限制 `HandlerConfiguration`)撤銷。

本章中的討論將集中在廢止用戶端認證上。
