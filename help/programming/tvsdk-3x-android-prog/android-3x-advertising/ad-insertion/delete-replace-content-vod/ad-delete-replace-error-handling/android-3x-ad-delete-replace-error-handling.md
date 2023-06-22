---
description: TVSDK會合併或重新排序不正確定義的時間範圍，以根據特定問題處理時間範圍錯誤。
title: 廣告刪除和取代錯誤處理
exl-id: 40d1cf67-df8c-4c5f-a1f2-defe3dd2b44a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 廣告刪除和取代錯誤處理  {#ad-deletion-and-replacement-error-handling}

TVSDK會合併或重新排序不正確定義的時間範圍，以根據特定問題處理時間範圍錯誤。

TVSDK管理 `timeRanges` 預設合併和重新排序程式時發生錯誤。 首先，播放器會依以下順序排序客戶定義的時間範圍： *開始* 時間。 根據此排序順序，如果範圍中有子集和交集，TVSDK會合併相鄰範圍並連線這些範圍。

TVSDK會使用下列選項來處理時間範圍錯誤：

* **順序不對** TVSDK會重新排序時間範圍。

* **子集** TVSDK會合併時間範圍子集。

* **相交** TVSDK會合併交集的時間範圍。

* **取代範圍衝突** TVSDK會選取最早的取代持續時間 `timeRange` 顯示在衝突群組中的物件。

TVSDK會以下列方式處理與廣告中繼資料的信令模式衝突：

* 如果廣告訊號模式與時間範圍中繼資料衝突，則時間範圍中繼資料一律有優先權。

   例如，如果廣告訊號模式設定為伺服器對應或資訊清單提示，且廣告中繼資料中還有MARK時間範圍，則產生的行為是範圍會加上標籤，且不會插入任何廣告。
* 對於REPLACE範圍，如果訊號模式設定為伺服器對應或資訊清單提示，則會按照REPLACE範圍中指定的方式取代範圍，而且不會透過伺服器對應或資訊清單提示插入廣告。

   如需詳細資訊，請參閱 *訊號模式/中繼資料組合行為* 表格於 [對從廣告訊號模式插入和刪除廣告的影響](../../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/delete-replace-content-vod/android-3x-signaling-mode-android.md).

請記住以下事項：

* 當伺服器未傳回有效值 `AdBreaks`，TVSDK會產生並處理 `NOPTimelineOperation` 空白的AdBreak，則不會播放任何廣告。

* 雖然C3廣告刪除/取代僅支援VOD，但若在廣告中繼資料中指定，也會為即時資料流處理時間範圍。
