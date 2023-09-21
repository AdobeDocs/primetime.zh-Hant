---
title: 處理授權退回請求
description: 處理授權退回請求
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# 處理授權退回請求{#handle-license-return-requests}

如果使用者端應用程式需要傳回授權，則會叫用 `DRMManager.returnVoucher()` Actionscript API可啟動此程式。 此API可在 `immediateCommit` 模式或 `confirmFirst` 模式。 如果 `immediateCommit` 設為 `true`，使用者端接著會立即刪除本機授權，而不需等待授權伺服器確認其已收到傳回授權的要求。 Adobe Primetime DRM授權伺服器應處理請求並將回應傳送給使用者端。 授權伺服器是否處理要求（例如減少指定使用者的授權計數）由授權伺服器決定。

* 要求處理常式類別為 `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler`
* 請求訊息類別為 `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage`

最小值 `Adobe Primetime DRM` 需要的SDK版本是第5版；請求URL是&quot; [!DNL /flashaccess/lreturn/v5]「。 和網域取消註冊一樣，伺服器會使用 `getRequestPhase()` 以判斷使用者端是否可預覽許可證回傳。
