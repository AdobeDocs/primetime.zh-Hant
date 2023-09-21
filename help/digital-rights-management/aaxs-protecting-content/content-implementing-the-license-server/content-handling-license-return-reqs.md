---
title: 處理授權退回要求
description: 處理授權退回要求
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# 處理授權退回要求{#handling-license-return-requests}

如果使用者端應用程式需要傳回授權，它會叫用DRMManager.returnVoucher() Actionscript API來啟動程式。 此API可在immediateCommit模式或confirmFirst模式中運作。 如果immediateCommit設定為true，使用者端將立即刪除本機授權，而不等待授權伺服器確認其已收到傳回授權的要求。 Adobe存取授權伺服器應處理該要求，並將回應傳送給使用者端。 授權伺服器是否實際對請求執行任何動作（例如減少指定使用者的授權計數）取決於授權伺服器。

* 要求處理常式類別是com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler
* 要求訊息類別為com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage

最低要求的Adobe存取SDK版本為第5版；請求URL將為» `/flashaccess/lreturn/v5`「。 如同「網域取消註冊」，伺服器應使用 `getRequestPhase()` 以判斷使用者端是否正在預覽授權退回。
