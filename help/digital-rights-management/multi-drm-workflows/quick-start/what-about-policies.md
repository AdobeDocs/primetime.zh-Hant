---
description: 設定策略是指定允許用戶何時以及如何播放受保護視頻內容的條件的過程。
title: 設定策略
exl-id: ab7295c8-88f2-4d4a-a7f1-3332df7bb735
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# 設定策略{#setting-policies}

設定策略是指定允許用戶何時以及如何播放受保護視頻內容的條件的過程。

策略建立作為許可證令牌請求的一部分進行。 (請參閱 [https://www.expressplay.com/developer/restapi/#widevine-license-token-request](https://www.expressplay.com/developer/restapi/#widevine-license-token-request) 例如，使用Widevine)。

一旦客戶的伺服器端代碼確定將頒發許可證（基於權利檢查、地理位置或任何其他必需資訊），它就會請求令牌， *標籤中* 它指定所需 `securityLevel`。 `hdcpOutputControl`, `licenseDuration`。 這些是Widevine策略的客戶端選項。 其他DRM解決方案提供了類似的方法，但每種情況的細節都不同，並在各個工作流中加以闡述。

>[!NOTE]
>
>Adobe提供了一個示例參考伺服器，它顯示如何實施您自己的權利伺服器/店面： [參考伺服器：示例ExpressPlay權利伺服器(SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)
