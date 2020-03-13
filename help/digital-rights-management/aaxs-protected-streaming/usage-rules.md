---
seo-title: 使用規則
title: 使用規則
uuid: 361d07b9-e4c8-47ab-8c45-a1de98c9fed7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 使用規則{#usage-rules}

使用Adobe Access Server for Protected Streaming，所有使用規則都會透過設定檔案在伺服器上指定。 受保護內容中指定的任何使用規則都會被覆寫，因此建議在內容封裝期間使用簡單的匿名原則。 可設定的使用規則可依每租用戶來設定。

Adobe Access Server for Protected Streaming支援下列使用規則：

* 輸出保護
* Adobe® AIR®、SWF、iOS和Android應用程式限制
* DRM和Runtime模組限制
* 越獄偵測實施（在支援越獄偵測的Adobe Access平台上）
* 授權快取預設會停用。 可以指定快取結束日期或允許時間快取（從核發授權時開始），來啟用授權快取。
* 多重播放權限，可讓您指定不同的輸出保護、應用程式限制和DRM/執行時期限制組合。 例如，可以通過使用帶有輸出保護的DRM模組限制為每個客戶端平台指定不同的輸出保護要求。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>若要支援遠端金鑰傳送至iOS裝置，封裝時使用的原則必須啟用遠端金鑰傳送。 此設定無法透過伺服器上的租用戶設定加以修改。 ***Adobe Primetime是建立可播放Adobe Access保護內容的iOS應用程式的必要工具。***

