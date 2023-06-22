---
title: 處理授權退回請求
description: 處理授權退回請求
copied-description: true
exl-id: c8813f7a-9a12-4c71-a945-cee73b6784fd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# 處理授權退回請求{#handling-license-return-requests}

如果使用者端應用程式需要傳回授權，它會叫用DRMManager.returnVoucher() Actionscript API來啟動程式。 此API可在immediateCommit模式或confirmFirst模式中運作。 如果immediateCommit設定為true，使用者端將立即刪除本機授權，而不等待授權伺服器確認其已收到傳回授權的要求。 Adobe存取授權伺服器應處理該要求，並將回應傳送給使用者端。 授權伺服器是否實際對請求執行任何動作（例如減少指定使用者的授權計數）取決於授權伺服器。

* 要求處理常式類別是com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler
* 要求訊息類別為com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage

最低要求的Adobe存取SDK版本為第5版；請求URL將為» `/flashaccess/lreturn/v5`「。 如同「網域取消註冊」，伺服器應使用 `getRequestPhase()` 以判斷使用者端是否正在預覽授權回傳。
