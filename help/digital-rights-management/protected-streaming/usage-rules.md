---
description: 使用Adobe Primetime DRM Server for Protected Streaming，您可以透過組態檔指定伺服器上的所有使用規則。
title: 關於使用規則
exl-id: 55af3a18-8fdb-4285-bd9f-ca479475e34f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---

# 關於使用規則{#about-usage-rules}

使用Adobe Primetime DRM Server for Protected Streaming，您可以透過組態檔指定伺服器上的所有使用規則。

受保護內容的DRM原則中指定的任何使用規則都會被覆寫。 因此，Adobe建議您在內容封裝期間使用簡單的匿名DRM原則。 您可以設定的任何使用規則都可以根據租使用者進行設定。

Primetime DRM Server for Protected Streaming支援下列使用規則：

* 輸出保護
* Adobe® AIR®、SWF、iOS和Android應用程式限制
* DRM和執行階段模組限制
* 支援越獄偵測的Primetime DRM平台上的越獄偵測強制執行
* 授權快取預設為停用。 您可以透過指定快取結束日期或允許快取的時間長度來啟用的授權快取；它會在發出授權時啟動。
* 多重播放許可權可讓您指定輸出保護、應用程式限制和DRM/執行階段限制的不同組合。 例如，您可以使用具有輸出保護的DRM模組限制，為每個使用者端平台指定不同的輸出保護要求。

>[!NOTE]
>
>如果您想要支援將遠端金鑰傳送至iOS裝置，則套用於封裝時的DRM政策必須啟用遠端金鑰傳送。 無法透過伺服器上的租使用者設定修改此設定。
