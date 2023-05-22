---
title: 處理許可證返回請求
description: 處理許可證返回請求
copied-description: true
exl-id: de577cb9-4ede-440e-8b71-1b39c6cc3c5b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# 處理許可證返回請求{#handle-license-return-requests}

如果客戶端應用程式需要返回許可證，則調用 `DRMManager.returnVoucher()` ActionScript API啟動進程。 此API可在 `immediateCommit` 或 `confirmFirst` 的子菜單。 如果 `immediateCommit` 設定為 `true`，然後客戶端立即刪除本地許可證，而不等待許可證伺服器確認它已接收到返回許可證的請求。 Adobe PrimetimeDRM許可證伺服器應處理該請求並向客戶端發送響應。 許可證伺服器是否處理該請求，例如減少指定用戶的許可證計數，由許可證伺服器決定。

* 請求處理程式類為 `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler`
* 請求消息類為 `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage`

最小 `Adobe Primetime DRM` 所需的SDK版本為5;請求URL為「」 [!DNL /flashaccess/lreturn/v5]。 與域註銷一樣，伺服器使用 `getRequestPhase()` 以確定客戶端是否可以預覽許可證返回。
