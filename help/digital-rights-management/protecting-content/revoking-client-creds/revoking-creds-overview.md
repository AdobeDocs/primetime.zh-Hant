---
seo-title: 概觀
title: 概觀
uuid: c6f54867-d0a3-43fd-9493-6496f1b7831a
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# 概述{#overview}

您可能需要撤銷客戶的憑據，或檢查給定的一組憑據是否已在特定條件下被撤銷。 如果證書受到危害，則可撤銷證書。 當發生這些問題時，授權將不再發給受損的客戶。

Adobe會維護「憑證撤銷清單」(CRL)，以撤銷受危害的客戶。 這些CRL由SDK自動執行。 許可伺服器可以通過禁止特定電腦認證或特定版本的DRM和運行時認證進一步限制客戶端。 可以建立`RevocationList`並傳入SDK以廢止電腦憑證。 通過在播放權中設定模組限制或通過在`HandlerConfiguration`中設定模組限制，可以在DRM策略級別撤銷特定DRM/運行時版本。

討論的中心是廢止用戶端認證。
