---
seo-title: 時間型規則概觀
title: 時間型規則概觀
uuid: 10b7766e-3b1a-4d8a-ba15-46976aa0847d
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# 時間型規則 {#time-based-rules}

Primetime DRM使用「軟執行」時間型授權限制。 如果時間右鍵在視訊播放期間過期，則Primetime DRM的預設行為是在下次重新建立視訊串流時（透過呼叫和），才限制 `Netstream.stop()` 播放 `Netstream.play()`。

雖然軟強制是預設行為，但您也可以執行下列任務之一，以啟用硬強制：

* 請您的視訊播放器定期輪詢授權，以確保沒有任何時間限制過期。 這可透過呼叫「錯誤 `DRMManager.loadVoucher(LOCAL_ONLY).` 碼」指出本機儲存的授權不再有效來完成。
* 每當使用者按一 **[!UICONTROL Pause]**&#x200B;下，您就可以錄制目前的視訊時間戳記，然後呼叫 `Netstream.stop()`。 當使用者按一下「播放」按鈕時，您可以尋找錄制的位置，然後呼叫 `Netstream.play()`。