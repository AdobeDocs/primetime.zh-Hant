---
title: 處理授權退貨請求
description: 處理授權退貨請求
copied-description: true
exl-id: de577cb9-4ede-440e-8b71-1b39c6cc3c5b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# 處理授權退貨請求{#handle-license-return-requests}

如果使用者端應用程式需要傳回授權，它會叫用 `DRMManager.returnVoucher()` 啟動程式的Actionscript API。 此API可在 `immediateCommit` 模式或 `confirmFirst` 模式。 若 `immediateCommit` 設為 `true`之後，使用者端會立即刪除本機授權，而不需等待授權伺服器確認其已收到傳回授權的要求。 Adobe Primetime DRM授權伺服器應處理請求並將回應傳送給使用者端。 授權伺服器是否處理要求（例如減少指定使用者的授權計數）由授權伺服器決定。

* 要求處理常式類別為 `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler`
* 請求訊息類別為 `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage`

最小值 `Adobe Primetime DRM` 所需的SDK版本為版本5；請求URL為&quot; [!DNL /flashaccess/lreturn/v5]「。 和網域取消註冊一樣，伺服器會使用 `getRequestPhase()` 以判斷使用者端是否可預覽授權回傳。
