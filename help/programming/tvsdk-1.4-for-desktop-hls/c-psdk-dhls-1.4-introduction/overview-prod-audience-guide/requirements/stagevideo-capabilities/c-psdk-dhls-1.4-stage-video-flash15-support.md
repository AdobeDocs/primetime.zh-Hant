---
description: 從Flash 15和更新版本開始，當沒有使用StageVideo進行硬體演算時，StageVideo會順暢地回到軟體StageVideo物件。
seo-description: 從Flash 15和更新版本開始，當沒有使用StageVideo進行硬體演算時，StageVideo會順暢地回到軟體StageVideo物件。
seo-title: Flash 15支援StageVideo
title: Flash 15支援StageVideo
uuid: 49bd8703-016e-4fda-8773-5254d4774ec6
translation-type: tm+mt
source-git-commit: fd686391df0fa711bba99bc1bc312c9ef619f184
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# Flash 15支援StageVideo{#flash-support-for-stagevideo}

從Flash 15和更新版本開始，當沒有使用StageVideo進行硬體演算時，StageVideo會順暢地回到軟體StageVideo物件。

請考慮以下有關Flash 15 StageVideo後援至軟體的資訊：

* 您的應用程式不需要變更程式碼。
* TVSDK不需要變更。

   您不需要TVSDK更新，就能使用StageVideo後援至軟體。
* 您的應用程式需要針對Flash 15重新編譯。
* 只要這些應用程式不使用Flash Player 15中新增的API，您為Flash 15重新編譯的應用程式就可繼續與Flash 14及更早版本搭配使用。

   如果您的Flash 14應用程式需要使用新的Flash 15 API，您必須以對象類型的轉換動態呼叫API，如此，應用程式在執行時期時就不會在Flash Player 14中失敗。

## HTML覆蓋{#html-overlays}

在Flash 15和更新版本中，當硬體StageVideo無法使用並回縮至軟體StageVideo時，您可維持HTML覆蓋的順暢顯示。 要啟用此功能，請設定`wmode=opaque`。

有些舊版瀏覽器不支援硬體加速。 如需這些需求的詳細資訊，請參閱[StageVideo最低需求](../../../../../tvsdk-1.4-for-desktop-hls/c-psdk-dhls-1.4-introduction/overview-prod-audience-guide/requirements/stagevideo-capabilities/r-psdk-dhls-1.4-requirements-stage-video.md)。 當您設定`wmode=opaque`時，會使用可影響效能的軟體StageVideo來呈現視訊。 通常，設定`wmode=direct`會直接將視訊轉譯為GPU，產生更佳的效能。 不過，這個選項也會覆寫HTML覆蓋。
