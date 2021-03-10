---
description: 使用Adobe PrimetimeDRM Server for Protected Streaming，您可以使用配置檔案指定伺服器上的所有使用規則。
title: 關於使用規則
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---


# 關於使用規則{#about-usage-rules}

使用Adobe PrimetimeDRM Server for Protected Streaming，您可以使用配置檔案指定伺服器上的所有使用規則。

在DRM策略中為受保護內容指定的任何使用規則都會被覆蓋。 因此，Adobe建議您在內容封裝期間使用簡單、匿名的DRM原則。 您可以設定的任何使用規則，皆可依每租用戶進行設定。

Primetime DRM Server for Protected Streaming支援下列使用規則：

* 輸出保護
* Adobe® AIR®、SWF、iOS和Android應用程式限制
* DRM和Runtime模組限制
* Primetime DRM平台上支援越獄偵測的越獄偵測實施
* 授權快取預設會停用。 您可以透過指定快取結束日期或允許快取時間量來啟用的授權快取；它會在授權發行時開始。
* 多重播放權限，可讓您指定不同的輸出保護、應用程式限制和DRM/執行時期限制組合。 例如，您可以使用DRM模組限制和輸出保護為每個客戶端平台指定不同的輸出保護要求。

>[!NOTE]
>
>如果您想要支援將遠端金鑰傳送至iOS裝置，則在封裝時套用的DRM政策必須啟用遠端金鑰傳送。 此設定無法透過伺服器上的租用戶設定加以修改。

