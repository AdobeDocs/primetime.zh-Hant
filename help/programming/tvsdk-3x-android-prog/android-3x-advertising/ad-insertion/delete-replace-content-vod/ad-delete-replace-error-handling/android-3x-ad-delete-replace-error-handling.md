---
description: TVSDK會根據特定問題來處理時間範圍錯誤，方法是合併或重新排序未正確定義的時間範圍。
seo-description: TVSDK會根據特定問題來處理時間範圍錯誤，方法是合併或重新排序未正確定義的時間範圍。
seo-title: 廣告刪除和取代錯誤處理
title: 廣告刪除和取代錯誤處理
uuid: 615f42b7-733a-49c4-bd7a-f14ad0d23fa0
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1

---


# 廣告刪除和取代錯誤處理 {#ad-deletion-and-replacement-error-handling}

TVSDK會根據特定問題來處理時間範圍錯誤，方法是合併或重新排序未正確定義的時間範圍。

TVSDK透過預 `timeRanges` 設的合併和重新排序程式來管理錯誤。 首先，播放器會依開始時間對客戶定義的時間 *範圍* 排序。 根據此排序順序，如果範圍間有子集和交集，TVSDK會合併相鄰範圍並連接這些範圍。

TVSDK可使用下列選項處理時間範圍錯誤：

* **TVSDK依順序** ，重新排序時間範圍。

* **子集** TVSDK會合併時間範圍子集。

* **Intersect** TVSDK會合併相交的時間範圍。

* **取代範圍衝突** TVSDK會從衝突群組中顯示的最早 `timeRange` 值選取取代持續時間。

TVSDK以下列方式處理與廣告中繼資料的信令模式衝突：

* 如果廣告信令模式與時間範圍元資料衝突，則時間範圍元資料始終具有優先順序。

   例如，如果廣告信令模式被設為伺服器地圖或資訊清單提示，而廣告中繼資料中也有MARK時間範圍，則產生的行為是已標籤範圍，且未插入廣告。
* 對於REPLACE範圍，如果信令模式被設定為伺服器映射或資訊清單提示，則該範圍將按照REPLACE範圍中指定的方式被替換，並且不會通過伺服器映射或資訊清單提示插入廣告。

   如需詳細資訊，請參閱「 *Effect on ad insertion and deletion from ad signaling mode（廣告插入和刪除效果）」中的「Signaling Mode / Metadata Combination Behaviors* （信令模式／元資料組合行為）」表 [](../../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/delete-replace-content-vod/android-3x-signaling-mode-android.md)。

請記住：

* 當伺服器未傳回有效 `AdBreaks`時，TVSDK會產生並處理空 `NOPTimelineOperation` 白AdBreak，且不會播放廣告。

* 雖然C3廣告刪除／取代僅支援VOD，但若在廣告中繼資料中指定，則即時串流也會處理時間範圍。
