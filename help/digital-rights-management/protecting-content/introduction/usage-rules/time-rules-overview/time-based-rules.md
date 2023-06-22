---
title: 時間型規則概觀
description: 時間型規則概觀
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# 時間型規則 {#time-based-rules}

Primetime DRM使用基於時間的授許可權制的「軟強制執行」。 如果右側時間在視訊播放期間到期，Primetime DRM的預設行為是在下次重新建立視訊資料流時才會限製播放(透過呼叫 `Netstream.stop()` 和 `Netstream.play()`)。

雖然軟性強制是預設行為，但您也可以透過執行下列工作之一來啟用硬性強制執行：

* 請您的視訊播放器定期輪詢授權，以確保時間限制沒有過期。 這可以透過呼叫來完成 `DRMManager.loadVoucher(LOCAL_ONLY).` 錯誤碼表示本機儲存的授權不再有效。
* 每當使用者點按 **[!UICONTROL Pause]**，您可以記錄目前的視訊時間戳記，然後呼叫 `Netstream.stop()`. 當使用者按一下「播放」按鈕時，您可以搜尋至記錄的位置，然後呼叫 `Netstream.play()`.