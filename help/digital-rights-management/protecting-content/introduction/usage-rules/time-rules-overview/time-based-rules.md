---
title: 基於時間的規則概述
description: 基於時間的規則概述
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# 基於時間的規則 {#time-based-rules}

黃金時段DRM使用基於時間的許可證限制的「軟強制」。 如果在播放視頻期間時間權限過期，則黃金時段DRM的預設行為是在下次重新建立視頻流之前(通過調用 `Netstream.stop()` 和 `Netstream.play()`)。

雖然軟強制是預設行為，但您也可以通過執行以下任務之一來啟用硬強制：

* 讓視頻播放器定期輪詢許可證，以確保時間限制均未過期。 可以通過調用 `DRMManager.loadVoucher(LOCAL_ONLY).` 錯誤代碼指示本地儲存的許可證不再有效。
* 只要用戶按一下 **[!UICONTROL Pause]**，您可以錄制當前視頻時間戳，然後調用 `Netstream.stop()`。 當用戶按一下「播放」按鈕時，您可以查找錄制的位置，然後撥打 `Netstream.play()`。