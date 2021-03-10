---
title: 使用規則
description: 使用規則
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# 使用規則{#usage-rules}

使用「保護串流的Adobe Access Server」，所有使用規則都會透過設定檔案在伺服器上指定。 受保護內容中指定的任何使用規則都會被覆寫，因此建議在內容封裝期間使用簡單的匿名原則。 可設定的使用規則可依每租用戶來設定。

「Adobe Access Server保護串流」支援下列使用規則：

* 輸出保護
* Adobe® AIR®、SWF、iOS和Android應用程式限制
* DRM和Runtime模組限制
* 越獄檢測強制(在支援越獄檢測的Adobe訪問平台上)
* 授權快取預設會停用。 可以指定快取結束日期或允許時間快取（從核發授權時開始），來啟用授權快取。
* 多重播放權限，可讓您指定不同的輸出保護、應用程式限制和DRM/執行時期限制組合。 例如，可以通過使用帶有輸出保護的DRM模組限制為每個客戶端平台指定不同的輸出保護要求。

>[!NOTE]
>
>若要支援遠端金鑰傳送至iOS裝置，封裝時使用的原則必須啟用遠端金鑰傳送。 此設定無法透過伺服器上的租用戶設定加以修改。 ***Adobe Primetime需要建立可播放Adobe存取保護內容的iOS應用程式。***

