---
title: 撤消客戶端憑據
description: 撤消客戶端憑據
copied-description: true
exl-id: 583dff28-c34a-4759-81a6-0471feab309f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# 撤消客戶端憑據{#revoking-client-credentials}

在某些情況下，必須撤消客戶端的憑據或檢查給定的一組憑據是否已被撤消。 如果憑據被破壞，則可撤銷憑據。 當這種情況發生時，許可證將不再發放給受損的客戶。

Adobe維護用於撤消受損客戶端的證書吊銷清單(CRL)。 這些CRL由SDK自動強制執行。 許可伺服器可以通過禁止特定電腦憑證或特定版本的DRM和運行時憑證進一步限制客戶機。 A `RevocationList` 可以建立並傳入SDK以撤消電腦憑據。 可在策略級別（通過在播放權中設定模組限制）或全局(通過在 `HandlerConfiguration`)。

本章中的討論將集中於撤消客戶端憑據。
