---
title: 處理許可證返回請求
description: 處理許可證返回請求
copied-description: true
exl-id: c8813f7a-9a12-4c71-a945-cee73b6784fd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# 處理許可證返回請求{#handling-license-return-requests}

如果客戶端應用程式需要返回許可證，它會調用DRMManager.returnVoucher()Actionscript API來啟動該進程。 此API可以在immediateCommit模式或confirmFirst模式下工作。 如果immediateCommit設定為true，則客戶端將立即刪除本地許可證，而無需等待許可證伺服器確認它已收到返回許可證的請求。 Adobe訪問許可證伺服器應處理該請求並向客戶端發送響應。 許可證伺服器是否實際對請求執行任何操作（例如減少給定用戶的許可證計數）取決於許可證伺服器。

* 請求處理程式類是com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler
* 請求消息類是com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage

所需的最低Adobe訪問SDK版本為5;請求URL將為&quot; `/flashaccess/lreturn/v5`。 與域註銷一樣，伺服器應使用 `getRequestPhase()` 以確定客戶端是否正在預覽許可證返回。
