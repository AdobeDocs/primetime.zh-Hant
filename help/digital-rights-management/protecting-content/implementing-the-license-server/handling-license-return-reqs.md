---
seo-title: 處理授權退貨要求
title: 處理授權退貨要求
uuid: 994df5af-476a-4ee8-b371-8900241be83d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# 處理授權退貨要求{#handle-license-return-requests}

如果客戶端應用程式需要返回許可證，則會調用`DRMManager.returnVoucher()` Actionscript API來啟動該過程。 此API可在`immediateCommit`模式或`confirmFirst`模式下運作。 如果`immediateCommit`設為`true`，則客戶端會立即刪除本地許可證，而無需等待許可證伺服器確認其已收到返回許可證的請求。 Adobe Primetime DRM授權伺服器應處理請求並傳送回應給用戶端。 授權伺服器是否處理請求，例如降低指定使用者的授權計數，由授權伺服器決定。

* 請求處理常式類別為`com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler`
* 請求消息類為`com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage`

`Adobe Primetime DRM` SDK版本的最低要求為5版；請求URL為&quot; [!DNL /flashaccess/lreturn/v5]&quot;。 與域取消註冊一樣，伺服器使用`getRequestPhase()`來確定客戶端是否可以預覽許可證返回。
