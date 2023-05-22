---
description: 瀏覽器TVSDK庫的通知部分允許您建立日誌記錄和調試系統，該系統可用於診斷和驗證目的。
title: 通知系統
exl-id: 6a3a3c56-1580-4f43-ba81-220a5b0fe5c3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# 通知系統 {#notification-system}

瀏覽器TVSDK庫的通知部分允許您建立日誌記錄和調試系統，該系統可用於診斷和驗證目的。

<!--<a id="section_EC5DBE8DDA434B70A01FA2F3EF4618BD"></a>-->

瀏覽器TVSDK具有 *無* API的策略。 大多數方法返回 `PSDKErrorCode` 值，以指示是否成功執行該方法。 要獲得所有可能的 `PSDKErrorCode` 值，請參閱瀏覽器TVSDK API引用。

通過特定事件通知非同步錯誤。

瀏覽器TVSDK派單 `MediaPlayer` 事件，提供有關播放器活動的資訊。 必須實現事件偵聽器以捕獲和響應這些事件。

>[!TIP]
>
>關鍵事件和資訊記錄在Web瀏覽器控制台上。

## 偵聽通知 {#section_06B96633433D497E842FB7ADD5F2C7DA}

您可以偵聽通知，並將您自己的通知添加到通知歷史記錄。 瀏覽器TVSDK通知系統的核心是 `Notification` 類，表示獨立通知。

要將應用程式設定為偵聽通知：

1. 使用MediaPlayer實例偵聽MediaPlayer狀態更改。

   ```js
   player.addEventListener( 
         AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. 實現回叫。

   回調接收的實例 `AdobePSDK.MediaPlayerStatusChangeEvent`，瀏覽器TVSDK將此事件對象傳遞到包含新播放器狀態的回調。
1. 您的應用程式可以通過使用 `MediaPlayer` 實例。
