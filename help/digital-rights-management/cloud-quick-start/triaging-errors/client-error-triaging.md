---
description: 有時候，內容無法播放。 任何情況都可能導致此情況，包括瀏覽器網路堆疊、傳輸層、作業系統、Flash Player執行階段或Primetime DRM系統中的錯誤。
title: 修剪錯誤概觀
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# 修剪錯誤{#triaging-errors}

有時候，內容無法播放。 任何情況都可能導致此情況，包括瀏覽器網路堆疊、傳輸層、作業系統、Flash Player執行階段或Primetime DRM系統中的錯誤。

第一診斷步驟是確定問題是否在沒有引入方程式的DRM加密的情況下顯現。 嘗試封裝內容，但請指示封裝者不要加密內容。 如果問題仍然存在，則可能是編碼或封裝內容或網路基礎架構中某處的問題。 如果在未加密的情況下封裝內容時，問題消失，播放失敗很可能是由於DRM問題，您應進行用戶端／伺服器修剪。

Primetime DRM（Primetime Cloud DRM以外）已推出數年。 因此，Primetime DRM的疑難排解與設定提供了大量社群來源資訊。 Adobe為Primetime DRM(先前稱為Adobe存取)使用者提供論壇，以匯整和分享問題與解決方案。 若要判斷您之前是否曾討論過您的問題，請檢查：[https://forums.adobe.com/community/adobe_access](https://forums.adobe.com/community/adobe_access)

## 客戶端錯誤診斷{#section_D0EBAEB0C27F4B01BD44124DEE62F6BA}

如果內容未播放，請檢查「範例視訊播放器」的右側面板，此面板將記錄發生的任何`DRMErrorEvent`。 如果有錯誤事件，則會與其中一個Flash Player執行階段錯誤產生關聯：

* [DRM客戶端錯誤消息參考](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages);或
* [AS3Flash執行階段錯誤](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html) （DRM問題始於3300）

