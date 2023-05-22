---
description: 從Flash15和更高版本，當沒有使用StageVideo的硬體呈現時，StageVideo將無縫地回退到軟體StageVideo對象。
title: Flash15支援StageVideo
exl-id: 23ef0806-3aa5-4c48-a4f7-4ad9b72bdcc9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# Flash15支援StageVideo{#flash-support-for-stagevideo}

從Flash15和更高版本，當沒有使用StageVideo的硬體呈現時，StageVideo將無縫地回退到軟體StageVideo對象。

請考慮以下有關Flash15 StageVideo回退到軟體的資訊：

* 應用程式中不需要代碼更改。
* 無需更改TVSDK。

   使用StageVideo回退到軟體不需要TVSDK更新。
* 您的應用程式需要重新編譯為15Flash。
* 您為Flash15重新編譯的應用程式將繼續與Flash14及更早版本配合使用，只要這些應用程式不使用Flash Player15中引入的任何新API。

   如果您的Flash14應用程式需要使用新的Flash15 API，則必須使用對象類型的轉換動態調用該API，以便應用程式在運行時不會在Flash Player14中失敗。

## HTML疊加 {#html-overlays}

在Flash15及更高版本中，當硬體StageVideo不可用並退回到軟體StageVideo時，您可以保持HTML疊加的無縫顯示。 要啟用此功能，請設定 `wmode=opaque`。

某些較舊的瀏覽器不支援硬體加速。 有關這些要求的詳細資訊，請參見 [StageVideo最低要求](../../../../../tvsdk-1.4-for-desktop-hls/c-psdk-dhls-1.4-introduction/overview-prod-audience-guide/requirements/stagevideo-capabilities/r-psdk-dhls-1.4-requirements-stage-video.md)。 設定 `wmode=opaque`，視頻採用StageVideo軟體進行渲染，這會影響效能。 通常，設定 `wmode=direct` 直接將視頻呈現到GPU，從而獲得更好的效能。 但是，此選項也覆蓋HTML覆蓋。
