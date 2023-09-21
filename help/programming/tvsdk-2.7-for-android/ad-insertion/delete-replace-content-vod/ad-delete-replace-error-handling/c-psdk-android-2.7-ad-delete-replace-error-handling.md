---
description: TVSDK會合併或重新排序定義錯誤的時間範圍，以根據特定問題處理時間範圍錯誤。
title: 廣告刪除和取代錯誤處理
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 概觀 {#ad-deletion-and-replacement-error-handling-overview}

TVSDK會合併或重新排序定義錯誤的時間範圍，以根據特定問題處理時間範圍錯誤。

TVSDK管理 `timeRanges` 透過預設合併和重新排序程式時發生錯誤。 首先，播放器會依 *開始* 時間。 根據此排序順序，如果範圍中有子集和交集，TVSDK會合併相鄰範圍並連線這些範圍。

TVSDK會使用下列選項來處理時間範圍錯誤：

* **順序不對** TVSDK會重新排序時間範圍。

* **子集** TVSDK會合併時間範圍子集。

* **相交** TVSDK會合併交集的時間範圍。

* **取代範圍衝突** TVSDK會選取最早的取代期間 `timeRange` 出現在衝突群組中。

TVSDK會以下列方式處理訊號模式與廣告中繼資料的衝突：

* 如果廣告訊號模式與時間範圍中繼資料衝突，則時間範圍中繼資料一律具有優先順序。

  例如，如果廣告訊號模式設定為伺服器地圖或資訊清單提示，且廣告中繼資料中還有MARK時間範圍，則結果行為是範圍會加上標籤，不會插入任何廣告。
* 對於REPLACE範圍，如果將訊號模式設定為伺服器對應或資訊清單提示，則會按照REPLACE範圍中指定的方式取代範圍，而且不會透過伺服器對應或資訊清單提示插入廣告。

  如需詳細資訊，請參閱 *訊號模式/中繼資料組合行為* 中的表格 [對從廣告訊號模式插入和刪除廣告的影響……](../../../../tvsdk-2.7-for-android/ad-insertion/delete-replace-content-vod/c-psdk-android-2.7-signaling-mode-metadata-combos-android.md#c_psdk_signaling-mode-metadata-combos-android).

請記住以下事項：

* 當伺服器未傳回有效資料時 `AdBreaks`， TVSDK會產生並處理 `NOPTimelineOperation` 對於空白的AdBreak，則不會播放任何廣告。

* 雖然C3廣告刪除/取代僅支援VOD，但若在廣告中繼資料中指定，也會為即時資料流處理時間範圍。
