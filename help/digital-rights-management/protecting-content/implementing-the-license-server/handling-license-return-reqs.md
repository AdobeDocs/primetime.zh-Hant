---
seo-title: 處理授權退貨要求
title: 處理授權退貨要求
uuid: 994df5af-476a-4ee8-b371-8900241be83d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 處理授權退貨要求{#handle-license-return-requests}

如果用戶端應用程式需要傳回授權，則會叫用 `DRMManager.returnVoucher()` Actionscript API來啟動程式。 此API可在模式 `immediateCommit` 或模式下 `confirmFirst` 運作。 如果 `immediateCommit` 設定為 `true`，則客戶端會立即刪除本地許可證，而不等待許可證伺服器確認其已收到返回許可證的請求。 Adobe Primetime DRM授權伺服器應處理請求並傳送回應給用戶端。 授權伺服器是否處理請求，例如降低指定使用者的授權計數，由授權伺服器決定。

* 請求處理常式類別為 `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler`
* 請求消息類為 `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage`

最低 `Adobe Primetime DRM` SDK版本為第5版；請求URL為「 [!DNL /flashaccess/lreturn/v5]」。 與「域取消註冊」一樣，伺服器用 `getRequestPhase()` 於確定客戶端是否可預覽許可證返回。
