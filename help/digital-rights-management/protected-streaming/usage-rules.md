---
description: 使用Adobe PrimetimeDRM Server for Protected Streaming，可以指定伺服器上所有使用規則以及配置檔案。
title: 關於使用規則
exl-id: 55af3a18-8fdb-4285-bd9f-ca479475e34f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---

# 關於使用規則{#about-usage-rules}

使用Adobe PrimetimeDRM Server for Protected Streaming，可以指定伺服器上所有使用規則以及配置檔案。

在DRM策略中為受保護內容指定的任何使用規則將被覆蓋。 因此，Adobe建議在內容打包期間使用簡單的匿名DRM策略。 您可以配置的任何使用規則都可以按租戶進行配置。

用於受保護流的黃金時段DRM伺服器支援以下使用規則：

* 輸出保護
* Adobe® AIR®、SWF、iOS和Android應用程式限制
* DRM和運行時模組限制
* 在支援越獄檢測的黃金時段DRM平台上執行越獄檢測
* 預設情況下禁用許可證快取。 允許通過指定快取結束日期或快取時間量來啟用的許可證快取；它從頒發許可證時開始。
* 多個播放權限，允許您指定輸出保護、應用程式限制和DRM/運行時限制的不同組合。 例如，可以使用帶輸出保護的DRM模組限制為每個客戶端平台指定不同的輸出保護要求。

>[!NOTE]
>
>如果要支援向iOS設備遠程密鑰傳遞，則在打包時應用的DRM策略必須啟用遠程密鑰傳遞。 無法通過伺服器上的租戶配置修改此設定。
