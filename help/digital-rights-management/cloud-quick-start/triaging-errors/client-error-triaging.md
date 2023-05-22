---
description: 偶爾，有時內容無法回放。 任何情況都可能導致此情況，包括瀏覽器網路堆棧、傳輸層、作業系統、Flash Player運行時或黃金時段DRM系統中的錯誤。
title: 篩選錯誤概述
exl-id: fe94d0a4-4f3c-4b0e-b830-a7a83bac1e85
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# 篩選錯誤 {#triaging-errors}

偶爾，有時內容無法回放。 任何情況都可能導致此情況，包括瀏覽器網路堆棧、傳輸層、作業系統、Flash Player運行時或黃金時段DRM系統中的錯誤。

第一診斷步驟是確定問題是否在沒有將DRM加密引入等式中的情況下顯現。 嘗試對內容進行打包，但請指示打包程式不要對內容進行加密。 如果問題仍然存在，則可能是編碼或打包內容或網路基礎架構中的某個位置出現問題。 如果在未加密的情況下打包內容時問題消失，則播放失敗可能是由於DRM問題，您應該參與客戶端/伺服器的篩選。

黃金時段DRM（黃金時段雲DRM之外）已進入市場數年。 因此，有大量關於故障排除和配置Mighine DRM的社區來源資訊。 Adobe為黃金時段DRM(以前稱為Adobe訪問)用戶提供了一個論壇，以聚合和分享問題和解決方案。 要確定以前是否討論過您的問題，請檢查： [https://forums.adobe.com/community/adobe_access](https://forums.adobe.com/community/adobe_access)

## 客戶端錯誤篩選 {#section_D0EBAEB0C27F4B01BD44124DEE62F6BA}

如果內容不播放，請檢查示例視頻播放器的右側面板，該面板將記錄任何 `DRMErrorEvent` 就發生了。 如果存在錯誤事件，它將與Flash Player運行時錯誤之一相關：

* [DRM客戶端錯誤消息參考](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages);或
* [AS3Flash運行時錯誤](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html) （DRM問題從3300開始）
