---
description: Adobe Access可與其他協力廠商內容串流解決方案搭配使用，以建立完整且安全的DRM媒體散發生態系統。
seo-description: Adobe Access可與其他協力廠商內容串流解決方案搭配使用，以建立完整且安全的DRM媒體散發生態系統。
seo-title: UltraViolet媒體與Adobe Access
title: UltraViolet媒體與Adobe Access
uuid: d287680f-02de-4cca-aeea-22b7fd8e67d2
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# UltraViolet媒體與Adobe Access {#ultraviolet-media-and-adobe-access}

Adobe Access可與其他協力廠商內容串流解決方案搭配使用，以建立完整且安全的DRM媒體散發生態系統。

UltraViolet( [](https://www.uvvu.com/))是數位版權驗證和雲端散發系統，可讓數位家庭娛樂內容的消費者透過多種平台和裝置串流及下載購買的內容。 UltraViolet內容將使用通用加密(CENC)以通用檔案格式(CFF)下載（或串流化）。

在Adobe Access中設定UltraViolet系統很容易。 下列使用案例描述內容流程行為：

<!--<a id="fig_cxy_dc2_44"></a>-->

![](assets/AdobeUV_web.png)

1. 內容擁有者會以CFF編碼並封裝內容。 套裝內容授權給零售商進行散發。
1. 零售商會將內容上傳至數位服務供應商，例如CDN。 內容現在可供下載。 請注意，其中某些角色可由一或多家公司擔任。

   使用者有支援Adobe AIR的裝置。 除此之外，用戶還需要安裝符合UltraViolet標準的應用程式。 應用程式包含解析CFF並呈現供執行階段使用的必要程式碼。 所有敏感加密操作都在安全運行時處理。
1. 應用程式可觸發裝置的網域連結，而裝置會與協調器互動。 協調員維護權限鎖、用戶資料庫和域。 協調者的網域管理員是使用Adobe Access SDK建立，以實施Adobe Access專用的網域加入／離開作業。
1. 然後，使用者可使用應用程式來選擇想要從零售商取得的視訊。 零售商通常提供入口網站並處理所有商業邏輯。
1. 然後零售商會與協調者互動，以新增權利Token。 零售商接著會將請求重新導向至服務供應商，以便實際下載內容。
1. 如果裝置尚未取得內容授權，則會使用CFF觸發授權要求。 該請求通常包括域證書、用戶證書和關於該應用程式的資訊。 該服務提供商運作的Adobe Access License Server（使用Adobe Access SDK）符合UltraViolet規格。
1. 服務提供商的UltraViolet業務邏輯根據需要與協調者交互以檢索適當的權限令牌，以確定是否應該發放內容許可。

   內容授權系結至網域。 用戶端應用程式可將授權插入CFF檔案。 現在，內容可在應用程式中播放，所有保護與使用規則實施都由Adobe Access元件在執行時期中處理。
1. 同一使用者擁有的其他裝置和應用程式可向協調者註冊。 內容現在可以載入至其他Adobe Access裝置，毋需進行任何外部交易。

