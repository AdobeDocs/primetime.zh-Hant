---
title: 關於證書
description: 關於證書
copied-description: true
exl-id: 24ca19bb-a71e-461a-9c3c-558d650e2d99
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# 關於證書 {#about-certificates}

Adobe PrimetimeDRM SDK可以在以下配置中使用：

* 黃金時段DRM製作SDK
* 黃金時段DRM評估SDK
* 黃金時段DRM試用版SDK

要使用Mogfire DRM SDK建立許可伺服器，必須從Adobe獲取數字證書。 數字證書（也簡稱為證書）將實體（如個人、組織或系統）綁定到特定的公共和私鑰對。 數字證書可以視為驗證個人、系統或組織身份的電子憑據。

為了在您的部署選項中實現最大的靈活性和增強的安全性，黃金時段DRM SDK需要四個證書：

* 許可證伺服器證書

   SDK使用此證書對發給客戶端的內容許可證進行簽名。
* 打包器證書

   SDK在打包（加密）內容時使用此證書生成DRM元資料。
* 傳輸證書

   SDK使用此證書來保護客戶端和許可證伺服器之間的通信。
* 域CA證書

   要實施域伺服器的客戶需要域CA證書。 與其他證書不同，域CA證書不是由Adobe頒發的。

>[!NOTE]
>
>對於評估SDK和試用版SDK，許可證伺服器、打包器和傳輸證書將合併為單個證書。
