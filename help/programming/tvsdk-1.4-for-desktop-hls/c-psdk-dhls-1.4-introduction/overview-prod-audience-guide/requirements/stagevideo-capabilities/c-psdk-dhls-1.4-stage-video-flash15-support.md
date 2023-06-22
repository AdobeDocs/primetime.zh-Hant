---
description: 從Flash15及更新版本開始，當無法使用StageVideo的硬體轉譯功能時，StageVideo會順暢地回覆為軟體StageVideo物件。
title: Flash15支援StageVideo
exl-id: 23ef0806-3aa5-4c48-a4f7-4ad9b72bdcc9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# Flash15支援StageVideo{#flash-support-for-stagevideo}

從Flash15及更新版本開始，當無法使用StageVideo的硬體轉譯功能時，StageVideo會順暢地回覆為軟體StageVideo物件。

請考慮下列有關Flash15 StageVideo後援軟體的資訊：

* 您的應用程式中不需要變更程式碼。
* 不需變更TVSDK。

   您不需要TVSDK更新即可使用StageVideo後援軟體。
* 您的應用程式需要重新編譯以進行Flash15。
* 您針對Flash15重新編譯的應用程式將繼續使用Flash14及舊版，前提是這些應用程式不使用Flash Player15中推出的任何新API。

   如果您的Flash14應用程式需要使用新的Flash15 API，您必須動態呼叫API，並將Object型別轉型為，讓應用程式在執行階段不會在Flash Player14中失敗。

## HTML覆蓋圖 {#html-overlays}

在Flash15和更新版本中，您可以在硬體StageVideo無法使用並回覆至軟體StageVideo時，維持順暢顯示HTML覆蓋圖。 若要啟用此功能，請設定 `wmode=opaque`.

某些舊版瀏覽器不支援硬體加速。 如需這些需求的詳細資訊，請參閱 [StageVideo最低需求](../../../../../tvsdk-1.4-for-desktop-hls/c-psdk-dhls-1.4-introduction/overview-prod-audience-guide/requirements/stagevideo-capabilities/r-psdk-dhls-1.4-requirements-stage-video.md). 當您設定時 `wmode=opaque`，影片會以StageVideo軟體呈現，而這會影響效能。 通常設定 `wmode=direct` 直接將視訊轉譯為GPU，進而獲得更優異的效能。 不過，此選項也會覆寫HTML覆蓋圖。
