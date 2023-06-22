---
description: 有時候，內容無法播放。 任何數量的情況都可能導致此問題，包括瀏覽器網路棧疊、傳輸層、作業系統、Flash Player執行階段或Primetime DRM系統發生錯誤。
title: 分類錯誤概觀
exl-id: fe94d0a4-4f3c-4b0e-b830-a7a83bac1e85
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# 正在判斷錯誤 {#triaging-errors}

有時候，內容無法播放。 任何數量的情況都可能導致此問題，包括瀏覽器網路棧疊、傳輸層、作業系統、Flash Player執行階段或Primetime DRM系統發生錯誤。

第一個診斷步驟是判斷問題是否顯示出來，而不需將DRM加密引入方程式。 嘗試封裝內容，但指示封裝程式不要加密內容。 如果問題仍然存在，可能是編碼或封裝內容或網路基礎架構中的某個位置發生問題。 如果在未加密的情況下封裝內容時問題消失，則播放失敗可能是由於DRM問題所導致，您應該進行使用者端/伺服器分級。

Primetime DRM （Primetime Cloud DRM以外）已上市數年。 因此，對於疑難排解和設定Primetime DRM，有大量的社群來源資訊。 Adobe為Primetime DRM (以前稱為Adobe存取)使用者提供了一個論壇，以彙總和分享問題和解決方案。 若要判斷先前是否討論過您的問題，請檢查： [https://forums.adobe.com/community/adobe_access](https://forums.adobe.com/community/adobe_access)

## 使用者端錯誤分級 {#section_D0EBAEB0C27F4B01BD44124DEE62F6BA}

如果內容沒有播放，請檢查範例視訊播放器的右側面板，其中會記錄任何 `DRMErrorEvent` 就會發生。 如果發生錯誤事件，則會與其中一個Flash Player執行階段錯誤相關聯：

* [DRM使用者端錯誤訊息參考](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)；或
* [AS3Flash執行階段錯誤](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html) （DRM問題開始於3300）
