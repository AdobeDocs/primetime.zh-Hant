---
title: 處理授權退貨要求
description: 處理授權退貨要求
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---


# 處理許可證返回請求{#handling-license-return-requests}

如果客戶端應用程式需要返回許可證，則會調用DRMManager.returnVoucher()Actionscript API來啟動該過程。 此API可在immediateCommit模式或confirmFirst模式下運作。 如果immediateCommit設定為true，則客戶端將立即刪除本地許可證，而無需等待許可證伺服器確認其已收到返回許可證的請求。 Adobe訪問許可證伺服器應處理請求並向客戶端發送響應。 授權伺服器是否實際對請求執行任何動作（例如降低特定使用者的授權計數），由授權伺服器決定。

* 請求處理常式類別為com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler
* 請求訊息類別為com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage

最低Adobe存取SDK版本為第5版；請求URL將為&quot; `/flashaccess/lreturn/v5`&quot;。 與域取消註冊一樣，伺服器應使用`getRequestPhase()`來確定客戶端是否正在預覽許可證返回。
