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

使用Adobe Access Server for Protected Streaming時，所有使用規則都是透過設定檔案在伺服器上指定。 受保護內容中指定的任何使用規則都會被覆寫，因此建議在內容封裝期間使用簡單的匿名原則。 可設定的使用規則可以根據租使用者進行設定。

適用於受保護串流的Adobe Access Server支援下列使用規則：

* 輸出保護
* Adobe® AIR®、SWF、iOS和Android應用程式限制
* DRM和執行階段模組限制
* 越獄偵測強制執行(在支援越獄偵測的Adobe存取平台上)
* 授權快取預設為停用。 可透過指定快取結束日期或允許快取的時間量（從發行授權時開始）來啟用授權快取。
* 多重播放許可權，可讓您指定輸出保護、應用程式限制和DRM/執行階段限制的不同組合。 例如，可以使用具有輸出保護的DRM模組限制，為每個使用者端平台指定不同的輸出保護要求。

>[!NOTE]
>
>若要支援將遠端金鑰傳遞至iOS裝置，封裝時採用的原則必須啟用遠端金鑰傳遞。 無法透過伺服器上的租使用者設定修改此設定。 ***建置可以播放受Adobe存取保護之內容的iOS應用程式需要Adobe Primetime。***
