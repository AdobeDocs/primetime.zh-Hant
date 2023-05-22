---
title: 概述
description: 概述
copied-description: true
exl-id: 332343ce-ac22-41a5-801a-3597476f0eaf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# 概述{#overview}

您可能需要撤消客戶端的憑據，或檢查給定的一組憑據是否已在特定條件下被撤消。 如果憑據被破壞，則可能會吊銷憑據。 當發生這些問題時，許可證將不再發放給受損的客戶。

Adobe維護用於撤消受損客戶端的證書吊銷清單(CRL)。 這些CRL由SDK自動強制執行。 許可伺服器可以通過禁止特定電腦憑證或特定版本的DRM和運行時憑證進一步限制客戶機。 A `RevocationList` 可以建立並傳入SDK以撤消電腦憑據。 通過在播放權中設定模組限制或通過在DRM策略級別中設定模組限制全局地撤消特定DRM/運行時版本 `HandlerConfiguration`。

討論的中心是撤消客戶端憑據。
