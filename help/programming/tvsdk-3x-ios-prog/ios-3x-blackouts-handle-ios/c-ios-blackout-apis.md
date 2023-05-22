---
description: TVSDK提供在實施封鎖期（包括方法、元資料和通知）時有用的API元素。
title: 封鎖API元素
exl-id: 76d99d8d-1aae-4faa-aaf2-bb7b535a1c71
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# 封鎖API元素 {#blackout-api-elements}

TVSDK提供在實施封鎖期（包括方法、元資料和通知）時有用的API元素。

在播放器中實施封鎖解決方案時，可以使用以下方法。

* **PTMediaPlayer**

   * `registerCurrentItemAsBackgroundItem` 將當前載入的資源另存為後台資源。 如果 `replaceCurrentItemWithPlayerItem` 在此方法之後調用，TVSDK將繼續下載後台項的清單，直到您調用 `unregisterCurrentBackgroundItem` 。 `stop`或 `reset` 。

   * `unregisterCurrentBackgroundItem` 將背景項設定為零，並停止提取和分析背景清單。

* **PTMetadata.PTBlackout元資料** A `PTMetadata` 特定於封鎖的類。

   這允許您設定不可查找的範圍( `CMTimeRanges`)。 TVSDK每次用戶查找時都檢查這些範圍。 如果設定了它，並且用戶尋求進入不可見範圍，則TVSDK強制查看器到不可見範圍的末尾。

* **下一頁開始** **PTAd元資料** 通過設定在即時流上啟用或禁用預滾動 `enableLivePreroll` 為「是」或「否」。 如果為否，則TVSDK在播放內容之前不會對預播廣告進行明確的廣告伺服器調用，因此不會播放預播。 這對中間輥沒有影響。 預設值為YES。

* **NSN工事**

   * `PTTimedMetadataChangedInBackgroundNotification`  — 當TVSDK檢測到後台清單中的訂閱標籤和新標籤時發佈 `PTTimedMetadata` 實例是從它準備的。 通知的對象是 `PTMediaPlayerItem` 當前正在播放的實例。 你可以 `PTTimedMetadata` 通知中的實例 `userInfo` 詞典 `PTTimedMetadataKey` 按鈕

   * `PTBackgroundManifestErrorNotification`  — 當媒體播放器完全無法載入後台清單時發佈，即所有流URL返回錯誤或無效響應。 通知的對象是 `PTMediaPlayerItem` 當前正在播放的實例。

* **PTN認證**

   * `BACKGROUND_MANIFEST_WARNING`

      * 代碼：204000
      * 類型：警告
      * 後台清單下載時出錯。
   * `INVALID_SEEK_WARNING` 在不可查範圍內嘗試查找時發送(在 `nonSeekableRanges` 設定 `PTBlackoutMetadata`)。
