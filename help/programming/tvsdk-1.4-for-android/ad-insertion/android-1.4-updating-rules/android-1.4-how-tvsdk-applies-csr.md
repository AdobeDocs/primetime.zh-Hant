---
description: TVSDK會以下列方式套用創意選取規則
title: 套用創意選取規則
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# 套用創意選取規則{#applying-creative-selection-rules}

TVSDK會透過下列方式套用創意選擇規則：

* TVSDK適用於所有 `default` 規則優先，之後是區域特定規則。
* TVSDK會忽略任何未針對目前區域ID定義的規則。
* 一旦TVSDK套用預設規則，區域特定規則即可根據 `host` （網域）相符的內容來自使用者選取的創意 `default` 規則。

* 在隨附的範例規則檔案中，一旦TVSDK套用 `default` 規則，如果M3U8創意網域不包含 [!DNL my.domain.com] 或 [!DNL a.bcd.com] 廣告區域為 `1234`，會重新排序創意內容，並先播放FlashVPAID創意內容（如果有的話）。 否則，會播放MP4廣告，依此類推，一直到JavaScript。

* 如果選取廣告創意，TVSDK無法原生播放( [!DNL .mp4]， [!DNL .flv]等)，TVSDK會發出重新封裝要求。

請注意，可由TVSDK處理的廣告型別仍需透過 `validMimeTypes` 設定於 `AuditudeSettings`.
