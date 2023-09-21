---
description: 設定原則是指定何時及如何允許使用者播放受保護視訊內容的程式。
title: 設定原則
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# 設定原則{#setting-policies}

設定原則是指定何時及如何允許使用者播放受保護視訊內容的程式。

原則建立是授權權杖請求的一部分。 (請參閱 [https://www.expressplay.com/developer/restapi/#widevine-license-token-request](https://www.expressplay.com/developer/restapi/#widevine-license-token-request) 例如，使用Widevine)。

一旦客戶的伺服器端程式碼判定將核發授權（根據權益檢查、地理位置或任何其他必要資訊）後，就會要求Token，並 *在權杖中* 它會指定必要的 `securityLevel`， `hdcpOutputControl`、和 `licenseDuration`. 這些是Widevine原則的使用者端選項。 其他DRM解決方案提供類似的方法，但每個案例的細節都不同，並在個別工作流程中加以詳述。

>[!NOTE]
>
>Adobe提供範例參考伺服器，說明如何實作您自己的軟體權利檔案伺服器/店面： [參考伺服器：範例ExpressPlay軟體權利檔案伺服器(SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)
