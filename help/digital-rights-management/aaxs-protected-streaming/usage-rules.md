---
title: 使用規則
description: 使用規則
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# 使用規則{#usage-rules}

使用Adobe Access Server for Protected Streaming時，所有使用規則都是透過設定檔在伺服器上指定。 受保護內容中指定的任何使用規則都會被覆寫，因此建議在內容封裝期間使用簡單的匿名原則。 可設定的使用規則可以根據每個租使用者進行設定。

適用於受保護串流的Adobe Access Server支援下列使用規則：

* 輸出保護
* Adobe® AIR®、SWF、iOS和Android應用程式限制
* DRM和執行階段模組限制
* 越獄偵測強制執行(在支援越獄偵測的Adobe存取平台上)
* 授權快取預設為停用。 可透過指定快取結束日期或允許快取的時間量（從發行授權時開始）來啟用授權快取。
* 多重播放許可權，可讓您指定「輸出保護」、「應用程式限制」和「DRM/執行階段限制」的不同組合。 例如，可以使用具有輸出保護的DRM模組限制，為每個使用者端平台指定不同的輸出保護要求。

>[!NOTE]
>
>若要支援將遠端金鑰傳送至iOS裝置，封裝時使用的原則必須啟用遠端金鑰傳送。 無法透過伺服器上的租使用者組態修改此設定。 ***建置可以播放受Adobe存取保護之內容的iOS應用程式需要Adobe Primetime。***
