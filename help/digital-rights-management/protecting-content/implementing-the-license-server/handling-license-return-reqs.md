---
title: 處理授權退貨要求
description: 處理授權退貨要求
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# 處理授權退貨要求{#handle-license-return-requests}

如果客戶端應用程式需要返回許可證，則會調用`DRMManager.returnVoucher()` Actionscript API來啟動該過程。 此API可在`immediateCommit`模式或`confirmFirst`模式下運作。 如果`immediateCommit`設為`true`，則客戶端會立即刪除本地許可證，而無需等待許可證伺服器確認其已收到返回許可證的請求。 Adobe PrimetimeDRM許可證伺服器應處理請求並向客戶端發送響應。 授權伺服器是否處理請求，例如降低指定使用者的授權計數，由授權伺服器決定。

* 請求處理常式類別為`com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler`
* 請求消息類為`com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage`

`Adobe Primetime DRM` SDK版本的最低要求為5版；請求URL為&quot; [!DNL /flashaccess/lreturn/v5]&quot;。 與域取消註冊一樣，伺服器使用`getRequestPhase()`來確定客戶端是否可以預覽許可證返回。
