---
title: 使用規則
description: 使用規則
copied-description: true
exl-id: 0f6df09f-47fd-4a05-bcb0-786beaba325a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# 使用規則{#usage-rules}

使用「受保護流」的Adobe Access Server，所有使用規則都通過配置檔案在伺服器上指定。 受保護內容中指定的任何使用規則都將被覆蓋，因此建議在內容打包期間使用簡單的匿名策略。 可配置的使用規則可以按租戶設定。

「受保護流」的Adobe Access Server支援以下使用規則：

* 輸出保護
* Adobe® AIR®、SWF、iOS和Android應用程式限制
* DRM和運行時模組限制
* 越獄檢測強制(在支援越獄檢測的Adobe訪問平台上)
* 預設情況下禁用許可證快取。 可以通過指定快取結束日期或允許時間快取（在發出許可證時開始）來啟用許可證快取。
* 多播放權限，用於指定輸出保護、應用程式限制和DRM/運行時限制的不同組合。 例如，可以使用帶輸出保護的DRM模組限制為每個客戶端平台指定不同的輸出保護要求。

>[!NOTE]
>
>要支援向iOS設備遠程密鑰傳遞，打包時使用的策略必須啟用遠程密鑰傳遞。 無法通過伺服器上的租戶配置修改此設定。 ***Adobe Primetime需要構建可播放Adobe訪問保護內容的iOS應用程式。***
