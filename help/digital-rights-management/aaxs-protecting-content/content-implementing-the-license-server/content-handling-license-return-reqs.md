---
seo-title: 處理授權退貨要求
title: 處理授權退貨要求
uuid: d184faea-88cb-44f3-a253-e5314d577f17
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 處理授權退貨要求{#handling-license-return-requests}

如果客戶端應用程式需要返回許可證，則會調用DRMManager.returnVoucher()Actionscript API來啟動該過程。 此API可在immediateCommit模式或confirmFirst模式下運作。 如果immediateCommit設定為true，則客戶端將立即刪除本地許可證，而無需等待許可證伺服器確認其已收到返回許可證的請求。 Adobe Access授權伺服器應處理要求並傳送回應給用戶端。 授權伺服器是否實際對請求執行任何動作（例如降低特定使用者的授權計數），由授權伺服器決定。

* 請求處理常式類別為com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler
* 請求訊息類別為com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage

所需的Adobe Access SDK最低版本為第5版；請求URL將為「 `/flashaccess/lreturn/v5`」。 與「域取消註冊」一樣，伺服器應使用 `getRequestPhase()` 來確定客戶端是否正在預覽許可證返回。
