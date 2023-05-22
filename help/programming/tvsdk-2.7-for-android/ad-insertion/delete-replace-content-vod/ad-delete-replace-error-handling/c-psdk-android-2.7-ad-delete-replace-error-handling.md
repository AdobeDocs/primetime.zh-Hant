---
description: TVSDK通過合併或重新排序未正確定義的時間範圍，根據特定問題處理時間範圍錯誤。
title: 廣告刪除和替換錯誤處理
exl-id: 0d70bb63-bdc5-4741-81db-1408216234c2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 概述 {#ad-deletion-and-replacement-error-handling-overview}

TVSDK通過合併或重新排序未正確定義的時間範圍，根據特定問題處理時間範圍錯誤。

TVSDK管理 `timeRanges` 預設合併和重新排序進程時出錯。 首先，玩家按 *開始* 時間。 根據此排序順序，如果範圍之間有子集和交集，則TVSDK合併相鄰範圍並連接這些範圍。

TVSDK使用以下選項處理時間範圍錯誤：

* **無序** TVSDK重新排序時間範圍。

* **子集** TVSDK合併時間範圍子集。

* **交叉** TVSDK合併相交時間範圍。

* **替換範圍衝突** TVSDK從最早的時間選擇替換持續時間 `timeRange` 在衝突組中顯示。

TVSDK通過以下方式處理與ad元資料的信令模式衝突：

* 如果廣告信令模式與時間範圍元資料衝突，則時間範圍元資料始終具有優先順序。

   例如，如果將廣告信令模式設定為伺服器映射或清單提示，並且廣告元資料中還存在MARK時間範圍，則所產生的行為是標籤了該範圍，並且不插入廣告。
* 對於REPLACE範圍，如果信令模式設定為伺服器映射或清單提示，則這些範圍將按REPLACE範圍中指定的方式替換，並且不會通過伺服器映射或清單提示插入廣告。

   有關詳細資訊，請參見 *信令模式/元資料組合行為* 表格 [從廣告信令模式對廣告插入和刪除的影響……](../../../../tvsdk-2.7-for-android/ad-insertion/delete-replace-content-vod/c-psdk-android-2.7-signaling-mode-metadata-combos-android.md#c_psdk_signaling-mode-metadata-combos-android)。

請記住以下內容：

* 當伺服器未返回有效時 `AdBreaks`, TVSDK生成並處理 `NOPTimelineOperation` 空的AdBreak，沒有廣告。

* 儘管C3和刪除/替換僅用於VOD，但如果在ad元資料中指定，則還會為即時流處理時間範圍。
