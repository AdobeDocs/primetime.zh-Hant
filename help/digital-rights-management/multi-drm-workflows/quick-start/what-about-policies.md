---
description: 設定原則是指指定使用者何時以及如何播放受保護視訊內容的程式。
seo-description: 設定原則是指指定使用者何時以及如何播放受保護視訊內容的程式。
seo-title: 設定策略
title: 設定策略
uuid: 2d2672ce-5ed4-4868-aa5e-0a9e21a809b3
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 設定策略{#setting-policies}

設定原則是指指定使用者何時以及如何播放受保護視訊內容的程式。

原則建立是您授權Token要求的一部分。 (如需使 [用Widevine的範例](https://www.expressplay.com/developer/restapi/#widevine-license-token-request) ，請參閱https://www.expressplay.com/developer/restapi/#widevine-license-token-request)。

一旦客戶的伺服器端程式碼判斷將核發授權（根據權益檢查、地理位置或任何其他必要資訊），則會要求代號，並在 *代號中指定* 必要、 `securityLevel`和 `hdcpOutputControl``licenseDuration`。 這些是Widevine策略的客戶端選項。 其他DRM解決方案提供類似的方法，但每種情況下的細節都不同，並在個別工作流程中加以闡述。

>[!NOTE]
>
>Adobe提供範例參考伺服器，說明如何實作您自己的權益伺服器／店面：參 [考伺服器：範例ExpressPlay Entitlement Server(SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)

